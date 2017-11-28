---
title: "Jak rozpocząć Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Przegląd dostępu uprzywilejowanego tożsamości z aplikacji Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="91315-103">Jak rozpocząć Przegląd dostępu w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="91315-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="91315-104">Przypisania ról nieodświeżone "", gdy użytkownicy mają uprzywilejowany dostęp, które nie wymagają już.</span><span class="sxs-lookup"><span data-stu-id="91315-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="91315-105">W celu zmniejszenia ryzyka związanego z tych przypisań ról starych, ról uprzywilejowanych powinni regularnie sprawdzić ról, którym przyznano użytkowników.</span><span class="sxs-lookup"><span data-stu-id="91315-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="91315-106">W tym dokumencie opisano kroki dotyczące uruchomienia Przegląd dostępu w usłudze Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="91315-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="91315-107">Rozpocząć Przegląd dostępu</span><span class="sxs-lookup"><span data-stu-id="91315-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="91315-108">Jeśli nie dodano aplikacji PIM do pulpitu nawigacyjnego w portalu Azure, zobacz kroki w [wprowadzenie do korzystania z usługi Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="91315-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="91315-109">Na stronie głównej aplikacji PIM istnieją trzy sposoby uruchamiania Przegląd dostępu:</span><span class="sxs-lookup"><span data-stu-id="91315-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="91315-110">**Dostęp do przeglądu** > **Dodaj**</span><span class="sxs-lookup"><span data-stu-id="91315-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="91315-111">**Role** > **przeglądu** przycisku</span><span class="sxs-lookup"><span data-stu-id="91315-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="91315-112">Wybierz określoną rolę, należy sprawdzić na liście ról > **przeglądu** przycisku</span><span class="sxs-lookup"><span data-stu-id="91315-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="91315-113">Po kliknięciu **Przejrzyj** przycisku **rozpocząć Przegląd dostępu** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="91315-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="91315-114">W tym bloku użytkownik chce skonfigurować przeglądu przy użyciu nazwy i limit czasu, wybierz rolę, aby przejrzeć i zdecydować, kto będzie wykonywać przeglądu.</span><span class="sxs-lookup"><span data-stu-id="91315-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Przegląd dostępu — zrzut ekranu Start][1]

### <a name="configure-the-review"></a><span data-ttu-id="91315-116">Skonfiguruj przeglądu</span><span class="sxs-lookup"><span data-stu-id="91315-116">Configure the review</span></span>
<span data-ttu-id="91315-117">Aby utworzyć Przegląd dostępu, należy nadaj jej nazwę i ustawiania datę początkową i końcową.</span><span class="sxs-lookup"><span data-stu-id="91315-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Skonfiguruj przeglądu — zrzut ekranu][2]

<span data-ttu-id="91315-119">Należy długość przeglądu wystarczająco długo, użytkowników ją zakończyć.</span><span class="sxs-lookup"><span data-stu-id="91315-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="91315-120">Jeśli zakończy się wcześniejsza od daty zakończenia, można zawsze zatrzymać przeglądu wcześniej.</span><span class="sxs-lookup"><span data-stu-id="91315-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="91315-121">Wybierz rolę do przeglądu</span><span class="sxs-lookup"><span data-stu-id="91315-121">Choose a role to review</span></span>
<span data-ttu-id="91315-122">Każdego przeglądu koncentruje się na tylko jedną rolę.</span><span class="sxs-lookup"><span data-stu-id="91315-122">Each review focuses on only one role.</span></span> <span data-ttu-id="91315-123">Chyba, że przegląd dostępu został uruchomiony z bloku konkretnej roli, należy wybrać rolę teraz.</span><span class="sxs-lookup"><span data-stu-id="91315-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="91315-124">Przejdź do **Przejrzyj członkostwo roli**</span><span class="sxs-lookup"><span data-stu-id="91315-124">Navigate to **Review role membership**</span></span>
   
    ![Przejrzyj członkostwo roli — zrzut ekranu][3]
2. <span data-ttu-id="91315-126">Wybierz jedną rolę z listy.</span><span class="sxs-lookup"><span data-stu-id="91315-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="91315-127">Zdecyduj, który przeprowadzi przeglądu</span><span class="sxs-lookup"><span data-stu-id="91315-127">Decide who will perform the review</span></span>
<span data-ttu-id="91315-128">Dostępne są trzy opcje umożliwiające wykonywanie przeglądu.</span><span class="sxs-lookup"><span data-stu-id="91315-128">There are three options for performing a review.</span></span> <span data-ttu-id="91315-129">Przegląd można przypisać do innej osoby, aby zakończyć, możesz zrobić to samodzielnie lub może mieć każdy użytkownik, Przejrzyj swoje własne dostępu.</span><span class="sxs-lookup"><span data-stu-id="91315-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="91315-130">Przejdź do **wybierz osób dokonujących przeglądu**</span><span class="sxs-lookup"><span data-stu-id="91315-130">Navigate to **Select reviewers**</span></span>
   
    ![Wybierz osoby dokonujące przeglądu — zrzut ekranu][4]
2. <span data-ttu-id="91315-132">Wybierz jedną z opcji:</span><span class="sxs-lookup"><span data-stu-id="91315-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="91315-133">**Wybierz osoby dokonującej przeglądu**: Użyj tej opcji, jeśli nie wiesz, który musi mieć dostęp.</span><span class="sxs-lookup"><span data-stu-id="91315-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="91315-134">Po wybraniu tej opcji można przypisać do właściciela zasobów lub menedżera grupy do ukończenia przeglądu.</span><span class="sxs-lookup"><span data-stu-id="91315-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="91315-135">**ME**: przydatne, jeśli chcesz obejrzeć, jak program access sprawdza pracy lub aby przejrzeć w imieniu osoby, które nie.</span><span class="sxs-lookup"><span data-stu-id="91315-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="91315-136">**Elementy członkowskie, zapoznaj się**: Użyj tej opcji, aby przejrzeć swoje własne przypisań ról użytkowników.</span><span class="sxs-lookup"><span data-stu-id="91315-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="91315-137">Uruchom przeglądu</span><span class="sxs-lookup"><span data-stu-id="91315-137">Start the review</span></span>
<span data-ttu-id="91315-138">Na koniec masz opcję, aby wymagać podania użytkowników przyczynę Jeśli udzielają dostępu.</span><span class="sxs-lookup"><span data-stu-id="91315-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="91315-139">Jeśli chcesz dodać opis przeglądu, a następnie wybierz **Start**.</span><span class="sxs-lookup"><span data-stu-id="91315-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="91315-140">Upewnij się, że poinformować użytkowników, wiadomo, że jest przegląd dostępu oczekiwanie na ich i wyświetlić je [jak przeprowadzić przegląd dostępu](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="91315-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="91315-141">Zarządzanie Przegląd dostępu</span><span class="sxs-lookup"><span data-stu-id="91315-141">Manage the access review</span></span>
<span data-ttu-id="91315-142">Postęp można śledzić w recenzentów zakończenia ich przeglądami na pulpicie nawigacyjnym usługi Azure AD PIM w sekcji przeglądami dostęp.</span><span class="sxs-lookup"><span data-stu-id="91315-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="91315-143">Brak praw dostępu zostaną zmienione w katalogu do [zakończeniu przeglądu](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="91315-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="91315-144">Aż do okresu przeglądu Przypomnij użytkowników przeprowadzenie ich przeglądu, lub Zatrzymaj przeglądu wcześniej w sekcji przeglądami dostępu.</span><span class="sxs-lookup"><span data-stu-id="91315-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="91315-145">PIM spis treści</span><span class="sxs-lookup"><span data-stu-id="91315-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
