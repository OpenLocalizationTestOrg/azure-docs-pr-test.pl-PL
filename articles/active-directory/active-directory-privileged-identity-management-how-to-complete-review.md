---
title: "Jak przeprowadzić przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Po rozpoczęciu Przegląd dostępu w usłudze Azure AD Privileged Identity Management Dowiedz się, jak zakończyć je i wyświetlić wyniki"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="7c3c3-103">Jak przeprowadzić przegląd dostępu w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="7c3c3-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="7c3c3-104">Administratorzy ról uprzywilejowanych można przejrzeć uprzywilejowanego dostępu raz [przeglądu zabezpieczeń została uruchomiona](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="7c3c3-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="7c3c3-105">Azure AD Privileged Identity Management (PIM) będzie automatycznie wysyłać wiadomości e-mail monitowania użytkowników, aby przejrzeć jego uprawnienia dostępu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="7c3c3-106">Jeśli użytkownik nie pobrały wiadomości e-mail, możesz wysłać je zgodnie z instrukcjami [jak przeprowadzić przegląd zabezpieczeń](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="7c3c3-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="7c3c3-107">Po umieszczeniu okresu przeglądu zabezpieczeń lub wszystkich użytkowników mają Zakończono ich własnym Przejrzyj, wykonaj kroki opisane w tym artykule, aby zarządzać przeglądu i wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="7c3c3-108">Zarządzanie inspekcje zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="7c3c3-108">Manage security reviews</span></span>
1. <span data-ttu-id="7c3c3-109">Przejdź do [portalu Azure](https://portal.azure.com/) i wybierz **Azure AD Privileged Identity Management** aplikacji na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="7c3c3-110">Wybierz **dostępu przeglądami** pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="7c3c3-111">Wybierz Przegląd dostępu, które mają być zarządzane.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="7c3c3-112">W bloku szczegółów przejrzyj dostępu istnieją liczba opcji zarządzania przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![Przyciski przeglądu dostępu PIM — zrzut ekranu][1]

### <a name="remind"></a><span data-ttu-id="7c3c3-114">Przypomnij</span><span class="sxs-lookup"><span data-stu-id="7c3c3-114">Remind</span></span>
<span data-ttu-id="7c3c3-115">Jeśli Przegląd dostępu jest skonfigurowana tak, aby użytkownicy Przejrzyj, **Przypomnij** przycisk wysyła powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="7c3c3-116">Stop</span><span class="sxs-lookup"><span data-stu-id="7c3c3-116">Stop</span></span>
<span data-ttu-id="7c3c3-117">Wszystkie przeglądy dostępu mają datę końcową, ale można użyć **zatrzymać** przycisk, aby zakończyć wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="7c3c3-118">Jeśli jeszcze nie zostały sprawdzone wszyscy użytkownicy tego czasu, będą mogli po zatrzymaniu przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="7c3c3-119">Nie można ponownie uruchomić przeglądu, po jest została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="7c3c3-120">Składanie wniosku o przyjęcie do programu</span><span class="sxs-lookup"><span data-stu-id="7c3c3-120">Apply</span></span>
<span data-ttu-id="7c3c3-121">Po zakończeniu Przegląd dostępu, ponieważ osiągnięto datę zakończenia lub zatrzymana go ręcznie, **Zastosuj** przycisk implementuje wyniku przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="7c3c3-122">Jeśli w przeglądzie nastąpiła odmowa dostępu użytkownika, to krok, który spowoduje usunięcie przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="7c3c3-123">Eksportowanie</span><span class="sxs-lookup"><span data-stu-id="7c3c3-123">Export</span></span>
<span data-ttu-id="7c3c3-124">Jeśli chcesz ręcznie zastosować wyników przeglądu zabezpieczeń, możesz wyeksportować przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="7c3c3-125">**Wyeksportować** przycisk rozpocznie się pobieranie pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="7c3c3-126">Wyniki w programie Excel lub inne programy, które mają otwarte pliki CSV można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="7c3c3-127">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="7c3c3-127">Delete</span></span>
<span data-ttu-id="7c3c3-128">Jeśli nie jest konieczne w żadnych późniejszych przeglądu, usuń go.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="7c3c3-129">**Usunąć** przycisk usuwa aplikacji PIM przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c3c3-130">Nie zostanie wyświetlone ostrzeżenie, zanim nastąpi jego usunięcia, dlatego upewnij się, że chcesz usunąć tego przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c3c3-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c3c3-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c3c3-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
