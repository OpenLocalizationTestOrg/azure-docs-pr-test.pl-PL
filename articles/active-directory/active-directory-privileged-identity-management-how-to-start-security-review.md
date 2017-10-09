---
title: "toostart aaaHow Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate dostępu Przejrzyj dla uprzywilejowanymi tożsamościami przy hello aplikacji Azure Privileged Identity Management."
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
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="ea957-103">Jak toostart dostępu Przejrzyj w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ea957-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="ea957-104">Przypisania ról nieodświeżone "", gdy użytkownicy mają uprzywilejowany dostęp, które nie wymagają już.</span><span class="sxs-lookup"><span data-stu-id="ea957-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="ea957-105">W kolejności tooreduce hello ryzyka związanego z tych przypisań ról starych ról uprzywilejowanych powinni regularnie sprawdzić hello ról, które użytkownicy mają prawo.</span><span class="sxs-lookup"><span data-stu-id="ea957-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="ea957-106">W tym dokumencie opisano kroki hello uruchamiania Przegląd dostępu w usłudze Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="ea957-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="ea957-107">Rozpocząć Przegląd dostępu</span><span class="sxs-lookup"><span data-stu-id="ea957-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="ea957-108">Jeśli nie dodano hello pulpit nawigacyjny tooyour aplikacji dla usługi PIM w hello portalu Azure, zobacz kroki hello w [wprowadzenie do korzystania z usługi Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="ea957-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="ea957-109">Z usługi PIM hello aplikacji strony głównej istnieją trzy sposoby toostart Przegląd dostępu:</span><span class="sxs-lookup"><span data-stu-id="ea957-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="ea957-110">**Dostęp do przeglądu** > **Dodaj**</span><span class="sxs-lookup"><span data-stu-id="ea957-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="ea957-111">**Role** > **przeglądu** przycisku</span><span class="sxs-lookup"><span data-stu-id="ea957-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="ea957-112">Wybierz hello konkretnej roli toobe usunięci z listy ról hello > **przeglądu** przycisku</span><span class="sxs-lookup"><span data-stu-id="ea957-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="ea957-113">Po kliknięciu hello **Przejrzyj** przycisk hello **rozpocząć Przegląd dostępu** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="ea957-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="ea957-114">W tym bloku jest będzie tooconfigure hello recenzowania o nazwie i limit czasu, wybraniu tooreview roli i zdecydować, kto będzie wykonywać hello przeglądu.</span><span class="sxs-lookup"><span data-stu-id="ea957-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Przegląd dostępu — zrzut ekranu Start][1]

### <a name="configure-hello-review"></a><span data-ttu-id="ea957-116">Skonfiguruj hello przeglądu</span><span class="sxs-lookup"><span data-stu-id="ea957-116">Configure hello review</span></span>
<span data-ttu-id="ea957-117">Przejrzyj dostępu toocreate należy tooname go i Ustaw daty początkową i końcową.</span><span class="sxs-lookup"><span data-stu-id="ea957-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Skonfiguruj przeglądu — zrzut ekranu][2]

<span data-ttu-id="ea957-119">Należy hello długość hello Przejrzyj wystarczająco długi dla toocomplete użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ea957-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="ea957-120">Jeśli zakończy się wcześniejsza niż data zakończenia hello, można zawsze zatrzymać przeglądu hello wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ea957-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="ea957-121">Wybierz tooreview roli</span><span class="sxs-lookup"><span data-stu-id="ea957-121">Choose a role tooreview</span></span>
<span data-ttu-id="ea957-122">Każdego przeglądu koncentruje się na tylko jedną rolę.</span><span class="sxs-lookup"><span data-stu-id="ea957-122">Each review focuses on only one role.</span></span> <span data-ttu-id="ea957-123">Jeśli nie został uruchomiony Przegląd dostępu hello bloku konkretnej roli, należy toochoose roli teraz.</span><span class="sxs-lookup"><span data-stu-id="ea957-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="ea957-124">Przejdź do zbyt**Przejrzyj członkostwo roli**</span><span class="sxs-lookup"><span data-stu-id="ea957-124">Navigate too**Review role membership**</span></span>
   
    ![Przejrzyj członkostwo roli — zrzut ekranu][3]
2. <span data-ttu-id="ea957-126">Wybierz jedną rolę z listy hello.</span><span class="sxs-lookup"><span data-stu-id="ea957-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="ea957-127">Zdecyduj, który przeprowadzi hello przeglądu</span><span class="sxs-lookup"><span data-stu-id="ea957-127">Decide who will perform hello review</span></span>
<span data-ttu-id="ea957-128">Dostępne są trzy opcje umożliwiające wykonywanie przeglądu.</span><span class="sxs-lookup"><span data-stu-id="ea957-128">There are three options for performing a review.</span></span> <span data-ttu-id="ea957-129">Można przypisać toosomeone przeglądu hello else toocomplete, możesz zrobić to samodzielnie lub może mieć każdy użytkownik, Przejrzyj swoje własne dostępu.</span><span class="sxs-lookup"><span data-stu-id="ea957-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="ea957-130">Przejdź do zbyt**wybierz osób dokonujących przeglądu**</span><span class="sxs-lookup"><span data-stu-id="ea957-130">Navigate too**Select reviewers**</span></span>
   
    ![Wybierz osoby dokonujące przeglądu — zrzut ekranu][4]
2. <span data-ttu-id="ea957-132">Wybierz jedną z opcji hello:</span><span class="sxs-lookup"><span data-stu-id="ea957-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="ea957-133">**Wybierz osoby dokonującej przeglądu**: Użyj tej opcji, jeśli nie wiesz, który musi mieć dostęp.</span><span class="sxs-lookup"><span data-stu-id="ea957-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="ea957-134">Po wybraniu tej opcji można przypisać właściciela zasobów tooa przeglądu hello lub toocomplete menedżera grupy.</span><span class="sxs-lookup"><span data-stu-id="ea957-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="ea957-135">**ME**: przydatne w przypadku toopreview jak dostępu przegląda pracy lub w imieniu osoby, które nie mają tooreview.</span><span class="sxs-lookup"><span data-stu-id="ea957-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="ea957-136">**Elementy członkowskie, zapoznaj się**: za pomocą przeglądu użytkowników hello toohave opcji własnych przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="ea957-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="ea957-137">Rozpocząć Przegląd hello</span><span class="sxs-lookup"><span data-stu-id="ea957-137">Start hello review</span></span>
<span data-ttu-id="ea957-138">Na koniec należy toorequire opcji hello użytkowników podać przyczynę, jeśli udzielają dostępu.</span><span class="sxs-lookup"><span data-stu-id="ea957-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="ea957-139">Jeśli chcesz dodać opis hello przeglądu, a następnie wybierz **Start**.</span><span class="sxs-lookup"><span data-stu-id="ea957-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="ea957-140">Upewnij się, że poinformować użytkowników, wiadomo, że jest przegląd dostępu oczekiwanie na ich i wyświetlić je [jak tooperform dostępu Przejrzyj](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="ea957-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="ea957-141">Zarządzanie hello Przegląd dostępu</span><span class="sxs-lookup"><span data-stu-id="ea957-141">Manage hello access review</span></span>
<span data-ttu-id="ea957-142">Możesz śledzić postępy hello w recenzentów hello zakończenia ich oceny w hello Azure AD PIM pulpitu nawigacyjnego, w hello dostępu przegląda sekcji.</span><span class="sxs-lookup"><span data-stu-id="ea957-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="ea957-143">Brak praw dostępu zostaną zmienione w katalogu hello do [zakończeniu Przejrzyj hello](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="ea957-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="ea957-144">Okresu przeglądu hello toocomplete użytkownicy mogą Przypomnij ich przeglądu, lub przejrzyj hello stop wczesne przed dostępem hello przegląda sekcji.</span><span class="sxs-lookup"><span data-stu-id="ea957-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="ea957-145">PIM spis treści</span><span class="sxs-lookup"><span data-stu-id="ea957-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
