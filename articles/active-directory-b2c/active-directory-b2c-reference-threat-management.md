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
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="e91c0-103">Usługa Azure Active Directory B2C: Zarządzanie zagrożeniami</span><span class="sxs-lookup"><span data-stu-id="e91c0-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="e91c0-104">Zarządzanie zagrożeniami obejmuje planowanie dotyczące ochrony przed atakami systemu i sieci.</span><span class="sxs-lookup"><span data-stu-id="e91c0-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="e91c0-105">Ataki typu "odmowa usługi" może spowodować zasobów niedostępny toointended użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e91c0-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="e91c0-106">Hasło ataków realizacji toounauthorized dostępu tooresources.</span><span class="sxs-lookup"><span data-stu-id="e91c0-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="e91c0-107">Usługa Azure Active Directory B2C (Azure AD B2C) ma wbudowane funkcje, które mogą pomóc chronić dane przed zagrożeniami tych na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="e91c0-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="e91c0-108">Ataki typu "odmowa usługi"</span><span class="sxs-lookup"><span data-stu-id="e91c0-108">Denial-of-service attacks</span></span>

<span data-ttu-id="e91c0-109">Wykrywanie i zapobieganie technik, takich jak pliki cookie SYN i szybkość i połączenia tooprotect limity bazowy zasobów przed atakami typu "odmowa usługi" korzysta z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e91c0-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="e91c0-110">Złamania hasła</span><span class="sxs-lookup"><span data-stu-id="e91c0-110">Password attacks</span></span>

<span data-ttu-id="e91c0-111">Usługa Azure AD B2C ma również techniki środki zaradcze w przypadku złamania hasła.</span><span class="sxs-lookup"><span data-stu-id="e91c0-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="e91c0-112">Środki zaradcze obejmuje ataków siłowych hasła i słownikowymi hasła.</span><span class="sxs-lookup"><span data-stu-id="e91c0-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="e91c0-113">Hasła, które są ustawiane przez użytkowników są wymagane toobe rozsądnych złożonych.</span><span class="sxs-lookup"><span data-stu-id="e91c0-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="e91c0-114">Za pomocą różnych sygnałów, usługi Azure AD B2C analizuje hello integralności żądań.</span><span class="sxs-lookup"><span data-stu-id="e91c0-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="e91c0-115">Usługa Azure AD B2C zaprojektowano toointelligently rozróżnianie uprawnionych użytkowników przed hakerami i zakłócanych.</span><span class="sxs-lookup"><span data-stu-id="e91c0-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="e91c0-116">Usługa Azure AD B2C zawiera toolock rozbudowanych strategii oparte na powitania haseł wpisanych prawdopodobieństwo atak powitania kont.</span><span class="sxs-lookup"><span data-stu-id="e91c0-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="e91c0-117">Aby uzyskać więcej informacji, odwiedź stronę hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="e91c0-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
