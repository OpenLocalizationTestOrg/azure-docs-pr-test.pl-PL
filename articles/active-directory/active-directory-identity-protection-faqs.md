---
title: "Ochronę tożsamości usługi Azure Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Azure AD Identity Protection"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 781f868c87cea3cd790d89c61e26eecf352babea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="0d98b-103">Ochronę tożsamości usługi Azure Active Directory — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="0d98b-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="0d98b-104">Dlaczego niektóre zdarzenia o podwyższonym ryzyku ma stanu "Closed (system)"</span><span class="sxs-lookup"><span data-stu-id="0d98b-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="0d98b-105">**Odpowiedź:** są to zdarzenia, które usługi Azure Active Directory Identity Protection wykryte i później zamknięta, ponieważ zdarzenia zostały już uważane za ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="0d98b-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because the events were no longer considered risky.</span></span> <span data-ttu-id="0d98b-106">Te zdarzenia nie wchodzą w skład poziom ryzyka użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0d98b-106">These events do not count towards the user’s risk level.</span></span> 

---

## <a name="do-i-need-to-be-a-global-admin-to-use-identity-protection-in-the-azure-portal"></a><span data-ttu-id="0d98b-107">Czy muszę być administratorem globalnym, aby korzystać z funkcji ochrony tożsamości w portalu Azure?</span><span class="sxs-lookup"><span data-stu-id="0d98b-107">Do I need to be a global admin to use Identity Protection in the Azure portal?</span></span>
<span data-ttu-id="0d98b-108">**Odpowiedź:** **nr**.</span><span class="sxs-lookup"><span data-stu-id="0d98b-108">**A:** **No**.</span></span> <span data-ttu-id="0d98b-109">Może być czytnik zabezpieczeń administratora zabezpieczeń lub administrator globalny, do korzystania z ochrony tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0d98b-109">You can either be a Security Reader, a Security Admin or a Global Admin to use Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="0d98b-110">Jak uzyskać Identity Protection?</span><span class="sxs-lookup"><span data-stu-id="0d98b-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="0d98b-111">**Odpowiedź:** zobacz [wprowadzenie do korzystania z usługi Azure Active Directory Premium](active-directory-get-started-premium.md) dla odpowiedzi na to pytanie.</span><span class="sxs-lookup"><span data-stu-id="0d98b-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="0d98b-112">Co się stanie po wygaśnięciu okresu próbnego usługi Azure Active Directory Premium 2?</span><span class="sxs-lookup"><span data-stu-id="0d98b-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="0d98b-113">**Odpowiedź:** Jeśli Twojej wersji próbnej usługi Azure Active Directory Premium 2 wygasł posiadanej wersji usługi Azure Active Directory bezpłatne, Basic lub 1 — wersja Premium, i ma włączoną ochroną za pomocą tożsamości, nadal masz do niego dostęp, nawet jeśli są niezgodne z licencjonowania.</span><span class="sxs-lookup"><span data-stu-id="0d98b-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access to it even though you are not in compliance with licensing.</span></span>

---
