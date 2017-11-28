---
title: Azure Active Directory Identity Protection aaaEnabling | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooenable Azure Active Directory Identity Protection."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: d26f466f5c7d6a425528a277d98c2c4b341ff8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="bbd9d-104">Włączenie ochrony tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbd9d-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="bbd9d-105">Azure Active Directory Identity Protection jest nową możliwość, która udostępnia skonsolidowany wgląd w podejrzane działania logowania i potencjalnych luk w zabezpieczeniach i przy użyciu powiadomień, zalecenia korygowania i ryzyka zasad pomaga chronić firmy.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="bbd9d-106">Witaj usługa wykrywa podejrzane działania dla użytkowników końcowych i tożsamości uprzywilejowanych (Administrator) oparte na sygnały jak metodą siłową ataków, wymuś ujawnione poświadczenia logowania z nieznanych lokalizacji zainfekowanych urządzeń, tooprotect względem tych działań w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-106">hello service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, tooprotect against these activities in real-time.</span></span> <span data-ttu-id="bbd9d-107">Co ważniejsze oparte na tych podejrzanych działań, ważność ryzyka użytkownika jest obliczana i ryzyka zasad można skonfigurować i automatycznie chronić hello tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect hello identities of your organization.</span></span> <span data-ttu-id="bbd9d-108">Aby uzyskać więcej informacji, zobacz [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="bbd9d-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="bbd9d-109">Tematy to pokazuje sposób tooenable Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-109">This topics shows how tooenable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-tooenable-azure-active-directory-identity-protection"></a><span data-ttu-id="bbd9d-110">Kroki tooenable Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bbd9d-110">Steps tooenable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="bbd9d-111">[Zaloguj się na](https://ms.portal.azure.com/) tooyour portalu Azure jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-111">[Sign-on](https://ms.portal.azure.com/) tooyour Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="bbd9d-112">W portalu Azure hello, kliknij przycisk **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-112">In hello Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="bbd9d-113">![Utwórz](./media/active-directory-identityprotection-enable/01.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="bbd9d-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="bbd9d-114">Kliknij na liście aplikacji hello **bezpieczeństwo i Obsługa tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-114">In hello applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="bbd9d-115">![Utwórz](./media/active-directory-identityprotection-enable/02.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="bbd9d-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="bbd9d-116">Kliknij przycisk **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="bbd9d-117">![Utwórz](./media/active-directory-identityprotection-enable/03.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="bbd9d-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="bbd9d-118">Na powitania **Azure AD Identity Protection** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bbd9d-118">On hello **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="bbd9d-119">![Utwórz](./media/active-directory-identityprotection-enable/04.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="bbd9d-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbd9d-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbd9d-120">Next Steps</span></span>
* [<span data-ttu-id="bbd9d-121">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbd9d-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

