---
title: Azure Active Directory Identity Protection powiadomienia | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak powiadomienia obsługują działaniach dochodzenia."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="e5605-104">Azure Active Directory Identity Protection powiadomienia</span><span class="sxs-lookup"><span data-stu-id="e5605-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="e5605-105">Azure AD Identity Protection wysyła dwa rodzaje automatycznych powiadomień e-mail w celu zarządzania ryzykiem użytkownika i zdarzenia ryzyka:</span><span class="sxs-lookup"><span data-stu-id="e5605-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="e5605-106">Użytkownik naruszony alertów e-mail</span><span class="sxs-lookup"><span data-stu-id="e5605-106">User compromised alert email</span></span>
* <span data-ttu-id="e5605-107">Wiadomość e-mail z podsumowaniem co tydzień</span><span class="sxs-lookup"><span data-stu-id="e5605-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="e5605-108">Użytkownik naruszony alertów e-mail</span><span class="sxs-lookup"><span data-stu-id="e5605-108">User compromised alert email</span></span>
<span data-ttu-id="e5605-109">Alert ze złamanymi zabezpieczeniami poczty e-mail użytkownika jest generowany, gdy usługi Azure AD Identity Protection zidentyfikuje konto, jako naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5605-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="e5605-110">Wiadomości e-mail zawiera łącze do użytkowników oflagowane ryzyka raportu na pulpicie nawigacyjnym Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="e5605-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="e5605-111">Zaleca się natychmiast Zbadaj powiadomienia, którego bezpieczeństwo zostało naruszone kont.</span><span class="sxs-lookup"><span data-stu-id="e5605-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="e5605-112">Wiadomość e-mail z podsumowaniem co tydzień</span><span class="sxs-lookup"><span data-stu-id="e5605-112">Weekly digest email</span></span>
<span data-ttu-id="e5605-113">Co tydzień wiadomość e-mail z podsumowaniem zawiera podsumowanie nowych zdarzeń ryzyka.</span><span class="sxs-lookup"><span data-stu-id="e5605-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="e5605-114">Obejmuje on:</span><span class="sxs-lookup"><span data-stu-id="e5605-114">It includes:</span></span>

* <span data-ttu-id="e5605-115">Narażeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="e5605-115">Users at risk</span></span>
* <span data-ttu-id="e5605-116">Podejrzane działania</span><span class="sxs-lookup"><span data-stu-id="e5605-116">Suspicious activities</span></span>
* <span data-ttu-id="e5605-117">Wykryto luk w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="e5605-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="e5605-118">Linki do powiązanych raportów w Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e5605-118">Links to the related reports in Identity Protection</span></span>

<br><span data-ttu-id="e5605-119">
![Korygowanie](./media/active-directory-identityprotection-notifications/400.png "korygowania")
</span><span class="sxs-lookup"><span data-stu-id="e5605-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="e5605-120">Możesz przełączyć wysyłania co tydzień wiadomość e-mail z podsumowaniem.</span><span class="sxs-lookup"><span data-stu-id="e5605-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="e5605-121">
![Ryzyko użytkownika](./media/active-directory-identityprotection-notifications/62.png "zagrożeń użytkownika")
</span><span class="sxs-lookup"><span data-stu-id="e5605-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="e5605-122">**Aby otworzyć okno dialogowe elementami konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="e5605-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="e5605-123">Na **Azure AD Identity Protection** bloku, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="e5605-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="e5605-124">
   ![Zasady użytkownika ryzyka](./media/active-directory-identityprotection-notifications/401.png "zasad ryzyka użytkownika")
   </span><span class="sxs-lookup"><span data-stu-id="e5605-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="e5605-125">W **ogólne** kliknij **powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="e5605-125">In the **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="e5605-126">
   ![Zasady użytkownika ryzyka](./media/active-directory-identityprotection-notifications/405.png "zasad ryzyka użytkownika")
   </span><span class="sxs-lookup"><span data-stu-id="e5605-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="e5605-127">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e5605-127">See also</span></span>
* [<span data-ttu-id="e5605-128">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5605-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
