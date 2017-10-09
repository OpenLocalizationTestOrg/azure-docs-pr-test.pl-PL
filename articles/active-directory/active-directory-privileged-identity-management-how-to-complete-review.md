---
title: "toocomplete aaaHow Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Po rozpoczęciu Przegląd dostępu w usłudze Azure AD Privileged Identity Management Dowiedz się jak toocomplete go i widoku hello wyników"
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
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="7c179-103">Jak toocomplete dostępu Przejrzyj w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="7c179-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="7c179-104">Administratorzy ról uprzywilejowanych można przejrzeć uprzywilejowanego dostępu raz [przeglądu zabezpieczeń została uruchomiona](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="7c179-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="7c179-105">Azure AD Privileged Identity Management (PIM) będzie automatycznie wysyłać wiadomości e-mail monitowania użytkowników tooreview dostępu.</span><span class="sxs-lookup"><span data-stu-id="7c179-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="7c179-106">Jeśli użytkownik nie pobrały wiadomości e-mail, możesz wysłać im instrukcje hello [jak tooperform zabezpieczeń Przejrzyj](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="7c179-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="7c179-107">Po umieszczeniu okresu przeglądu zabezpieczeń hello lub wszyscy użytkownicy hello zostało ukończone w ich własnym Przejrzyj, wykonaj kroki hello w tym przeglądzie hello toomanage artykułu i zobaczyć wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7c179-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="7c179-108">Zarządzanie inspekcje zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="7c179-108">Manage security reviews</span></span>
1. <span data-ttu-id="7c179-109">Przejdź toohello [portalu Azure](https://portal.azure.com/) i wybierz hello **Azure AD Privileged Identity Management** aplikacji na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="7c179-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="7c179-110">Wybierz hello **dostępu przeglądami** sekcji hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7c179-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="7c179-111">Wybierz hello Przegląd dostępu, które mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="7c179-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="7c179-112">W bloku szczegółów Przegląd dostępu hello istnieją liczba opcji zarządzania przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c179-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![Przyciski przeglądu dostępu PIM — zrzut ekranu][1]

### <a name="remind"></a><span data-ttu-id="7c179-114">Przypomnij</span><span class="sxs-lookup"><span data-stu-id="7c179-114">Remind</span></span>
<span data-ttu-id="7c179-115">Jeśli Przegląd dostępu jest skonfigurowana tak, aby użytkownicy hello Przejrzyj samodzielnie, hello **Przypomnij** przycisk wysyła powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="7c179-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="7c179-116">Stop</span><span class="sxs-lookup"><span data-stu-id="7c179-116">Stop</span></span>
<span data-ttu-id="7c179-117">Wszystkie przeglądy dostępu mają datę końcową, ale można użyć hello **zatrzymać** toofinish przycisk go wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7c179-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="7c179-118">Jeśli jeszcze nie zostały sprawdzone wszyscy użytkownicy tego czasu, nie będą tooafter może zatrzymać hello przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c179-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="7c179-119">Nie można ponownie uruchomić przeglądu, po jest została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="7c179-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="7c179-120">Składanie wniosku o przyjęcie do programu</span><span class="sxs-lookup"><span data-stu-id="7c179-120">Apply</span></span>
<span data-ttu-id="7c179-121">Po zakończeniu przeglądu dostęp, albo ponieważ osiągnięto datę zakończenia hello lub go ręcznie, zatrzymana hello **Zastosuj** przycisk implementuje hello wyniku hello przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c179-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="7c179-122">Jeśli w przeglądzie hello nastąpiła odmowa dostępu użytkownika, jest to krok hello spowoduje usunięcie przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="7c179-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="7c179-123">Eksportowanie</span><span class="sxs-lookup"><span data-stu-id="7c179-123">Export</span></span>
<span data-ttu-id="7c179-124">Jeśli chcesz ręcznie tooapply hello wyników przeglądu zabezpieczeń hello, możesz wyeksportować hello przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c179-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="7c179-125">Witaj **wyeksportować** przycisk rozpocznie się pobieranie pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="7c179-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="7c179-126">Wyniki hello w programie Excel lub inne programy, które mają otwarte pliki CSV można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="7c179-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="7c179-127">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="7c179-127">Delete</span></span>
<span data-ttu-id="7c179-128">Jeśli nie jesteś zainteresowany hello przejrzyj wszelkie dodatkowe, usuń go.</span><span class="sxs-lookup"><span data-stu-id="7c179-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="7c179-129">Witaj **usunąć** przycisk usuwa hello PIM aplikacji hello przeglądu.</span><span class="sxs-lookup"><span data-stu-id="7c179-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c179-130">Zostanie nie wyświetlone ostrzeżenie, zanim nastąpi jego usunięcia, dlatego należy się, że toodelete, który sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="7c179-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c179-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c179-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
