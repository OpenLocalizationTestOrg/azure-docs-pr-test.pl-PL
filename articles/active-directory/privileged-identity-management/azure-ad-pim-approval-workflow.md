---
title: "Azure Privileged Identity Management przepływów pracy | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przepływów pracy w zarządzania tożsamości uprzywilejowanych (PIM)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="cc0b1-103">Zatwierdzenia (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="cc0b1-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="cc0b1-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cc0b1-104">Overview</span></span>

<span data-ttu-id="cc0b1-105">Z zatwierdzenia Privileged Identity Management można skonfigurować role, aby wymagały zatwierdzenia aktywacji i wybierz jednego lub wielu użytkowników lub grup w ramach delegowanego osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="cc0b1-106">Zachowaj odczytu, aby dowiedzieć się, jak skonfigurować role i wybierz osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="cc0b1-107">Pamiętaj, ta funkcja jest nadal w rozwoju i mogą wystąpić błędy.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="cc0b1-108">Funkcji, łącznie z tekstem i konwencje nazewnictwa mogą ulec zmianie, a nie należy traktować jako ostatecznego.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="cc0b1-109">Kluczową terminologię</span><span class="sxs-lookup"><span data-stu-id="cc0b1-109">Key Terminology</span></span>

<span data-ttu-id="cc0b1-110">*Kwalifikujące się roli użytkownika* — kwalifikujących się roli użytkownik jest użytkownikiem w organizacji, który jest przypisany do roli usługi Azure AD jako kwalifikujących się (rola wymaga aktywacji).</span><span class="sxs-lookup"><span data-stu-id="cc0b1-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="cc0b1-111">*Delegowane osoba zatwierdzająca* — delegowanego osoba zatwierdzająca jest jednego lub wielu osób lub grup w ramach usługi Azure AD, odpowiedzialnych za zatwierdzanie żądań dla roli aktywacji.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="cc0b1-112">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="cc0b1-112">Scenarios</span></span>

<span data-ttu-id="cc0b1-113">Prywatnej wersji zapoznawczej obsługuje następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="cc0b1-114">**Jako uprzywilejowane roli administratora pararozaniliny można wykonywać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cc0b1-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="cc0b1-115">Włącz zatwierdzenia dla określonych ról</span><span class="sxs-lookup"><span data-stu-id="cc0b1-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="cc0b1-116">Określ osoba zatwierdzająca użytkowników i grupy, aby zatwierdzić żądań</span><span class="sxs-lookup"><span data-stu-id="cc0b1-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="cc0b1-117">Wyświetl historię żądań i zatwierdzania dla wszystkich ról uprzywilejowanych</span><span class="sxs-lookup"><span data-stu-id="cc0b1-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="cc0b1-118">**Wyznaczone osoby zatwierdzającej można:**</span><span class="sxs-lookup"><span data-stu-id="cc0b1-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="cc0b1-119">Wyświetlanie oczekujących zatwierdzeń (liczba żądań)</span><span class="sxs-lookup"><span data-stu-id="cc0b1-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="cc0b1-120">Zatwierdzanie lub odrzucanie żądań w celu podniesienia roli (pojedynczego i/lub masowo)</span><span class="sxs-lookup"><span data-stu-id="cc0b1-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="cc0b1-121">Podaj uzasadnienie dla moich lub odrzuceniu</span><span class="sxs-lookup"><span data-stu-id="cc0b1-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="cc0b1-122">**Kwalifikujące się roli użytkownika może:**</span><span class="sxs-lookup"><span data-stu-id="cc0b1-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="cc0b1-123">żądanie aktywacji roli, która wymaga zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="cc0b1-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="cc0b1-124">Wyświetl stan żądanie aktywacji</span><span class="sxs-lookup"><span data-stu-id="cc0b1-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="cc0b1-125">wykonać zadanie w usłudze Azure AD, jeśli Aktywacja została zatwierdzona</span><span class="sxs-lookup"><span data-stu-id="cc0b1-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="cc0b1-126">Nawigacji</span><span class="sxs-lookup"><span data-stu-id="cc0b1-126">Navigation</span></span>

<span data-ttu-id="cc0b1-127">Zaktualizowaliśmy nawigacji do obsługi zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="cc0b1-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="cc0b1-128">Domyślna strona początkowa zapewnia wygodny dostęp do informacji na temat usługi PIM oraz Nowa dokumentacja zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="cc0b1-129">Dodaliśmy również nową sekcję dla wszystkich użytkowników PIM, "Moje Historia inspekcji".</span><span class="sxs-lookup"><span data-stu-id="cc0b1-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="cc0b1-130">W tym miejscu znajdziesz wszystkie informacje istotne dla Twojej tożsamości.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="cc0b1-131">W tym wszystkie swoje żądania oczekujące i ukończone, wszelkich decyzji podjętych dotyczące żądań, które należy rozwiązać i wszystkich poprzednich aktywacji roli w jednej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="cc0b1-132">Włącz zatwierdzenia dla określonych ról</span><span class="sxs-lookup"><span data-stu-id="cc0b1-132">Enable approval for specific roles</span></span>

<span data-ttu-id="cc0b1-133">Aby włączyć zatwierdzenia dla konkretnej roli, należy najpierw wybrać role katalogu z lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="cc0b1-134">Znajdź i wybierz ustawienia w obszarze nawigacji po lewej stronie ról katalogu</span><span class="sxs-lookup"><span data-stu-id="cc0b1-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="cc0b1-135">Wybierz role uprzywilejowane:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="cc0b1-136">Zaznacz pole wyboru "Włącz" w wymagają zatwierdzenia sekcji:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="cc0b1-137">Po włączeniu bloku rozwinie się następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="cc0b1-138">Jeśli nie określono żadnych osób zatwierdzających, PRA(s) stają się osoby zatwierdzające domyślne.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="cc0b1-139">PRA(s) będzie potrzebować zatwierdzić wszystkie żądania aktywacji dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="cc0b1-140">Określ osoba zatwierdzająca użytkowników i grupy, aby zatwierdzić żądań</span><span class="sxs-lookup"><span data-stu-id="cc0b1-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="cc0b1-141">Aby delegować zatwierdzenia, kliknij opcję "Wybierz osób zatwierdzających":</span><span class="sxs-lookup"><span data-stu-id="cc0b1-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="cc0b1-142">Podczas ładowania bloku wybierz osób zatwierdzających może wyszukać określonego użytkownika lub grupy za pomocą pasek wyszukiwania w górnej lub wybierając z listy wstępnie wypełniane, a następnie kliknij "Wybierz" po zakończeniu:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="cc0b1-143">Uwaga: Można wybrać wielu użytkowników lub grup w czasie.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="cc0b1-144">Wybór będą wyświetlane na liście wybranych osób zatwierdzających, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="cc0b1-145">Aby usunąć osoba zatwierdzająca, po prostu kliknij przycisk Usuń przy jego nazwie.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="cc0b1-146">Aby dodać dodatkowe osób zatwierdzających, powtórz ten proces.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="cc0b1-147">Wyświetl historię żądań i zatwierdzania dla wszystkich ról uprzywilejowanych</span><span class="sxs-lookup"><span data-stu-id="cc0b1-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="cc0b1-148">Aby wyświetlić historię żądania i zatwierdzania dla wszystkich ról uprzywilejowanych, wybierz Historia inspekcji na pulpicie nawigacyjnym:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="cc0b1-149">Sortowanie danych w ramach akcji i wyszukaj "Zatwierdzone aktywacji"</span><span class="sxs-lookup"><span data-stu-id="cc0b1-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="cc0b1-150">Wyświetlanie oczekujących zatwierdzeń (liczba żądań)</span><span class="sxs-lookup"><span data-stu-id="cc0b1-150">View pending approvals (requests)</span></span>

<span data-ttu-id="cc0b1-151">Zatwierdzającą delegowanego będzie otrzymywał powiadomienia e-mail, kiedy żądanie oczekuje na zatwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="cc0b1-152">Aby wyświetlić te żądania w portalu usługi PIM, z poziomu pulpitu nawigacyjnego (w obszarze nawigacji nowe) wybierz kartę "Oczekujących żądań zatwierdzenia" na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="cc0b1-153">Z tego miejsca zobaczysz listę żądania w oczekiwaniu na zatwierdzenie:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="cc0b1-154">Zatwierdzanie lub odrzucanie żądań w celu podniesienia roli (pojedynczego i/lub masowo)</span><span class="sxs-lookup"><span data-stu-id="cc0b1-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="cc0b1-155">Wybierz żądania, które chcesz zaakceptować lub odrzucić, a następnie kliknij przycisk w pasku akcji, który odpowiada decyzji:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="cc0b1-156">Podaj uzasadnienie dla moich lub odrzuceniu</span><span class="sxs-lookup"><span data-stu-id="cc0b1-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="cc0b1-157">Spowoduje to otwarcie nowego bloku na zatwierdzenie lub odrzucenie jednocześnie wiele żądań.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="cc0b1-158">Wprowadź uzasadnienie decyzji, a następnie kliknij przycisk Zatwierdź (lub odmawiać zezwolenia) u dołu lub bloku:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="cc0b1-159">Po zakończeniu procesu żądania symbolu stanu będzie odzwierciedlać wprowadzone decyzji (w tym przykładzie decyzji jest zatwierdzić):</span><span class="sxs-lookup"><span data-stu-id="cc0b1-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="cc0b1-160">Żądania aktywacji roli, która wymaga zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="cc0b1-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="cc0b1-161">Mogą zostać rozpoczęte żądają aktywacji roli, która wymaga zatwierdzenia od starego nawigacji PIM lub nowe nawigacji, ponieważ proces aktywacji roli jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="cc0b1-162">Po prostu wybierz rolę z listy ról do aktywacji:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="cc0b1-163">Jeśli ról uprzywilejowanych wymaga uwierzytelniania wieloskładnikowego, zostanie wyświetlony monit przeprowadzenie tego zadania:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="cc0b1-164">Po jego zakończeniu, kliknij przycisk Aktywuj i uzasadnić (jeśli jest to wymagane):</span><span class="sxs-lookup"><span data-stu-id="cc0b1-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="cc0b1-165">Obiekt żądający zostanie wyświetlone powiadomienie, że żądanie oczekuje na zatwierdzenie:</span><span class="sxs-lookup"><span data-stu-id="cc0b1-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="cc0b1-166">Wyświetl stan żądanie aktywacji</span><span class="sxs-lookup"><span data-stu-id="cc0b1-166">View the status of your request to activate</span></span>

<span data-ttu-id="cc0b1-167">Wyświetlanie stanu oczekującego żądania, aby aktywować musi być dostępny z nowego nawigacji.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="cc0b1-168">Na pasku nawigacyjnym po lewej stronie wybierz kartę "Moje żądania":</span><span class="sxs-lookup"><span data-stu-id="cc0b1-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="cc0b1-169">Stan żądania domyślnie przyjmowana jest jako "Oczekujące", ale można Przełącz, aby wyświetlić wszystkie lub odrzucone żądania.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="cc0b1-170">Wykonać zadanie w usłudze Azure AD, jeśli Aktywacja została zatwierdzona</span><span class="sxs-lookup"><span data-stu-id="cc0b1-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="cc0b1-171">Gdy żądanie zostanie zatwierdzone, rola jest aktywna i może kontynuować pracę, która wymaga tej roli.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="cc0b1-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc0b1-172">Next steps</span></span>

<span data-ttu-id="cc0b1-173">Twoja opinia jest przydatna do nas.</span><span class="sxs-lookup"><span data-stu-id="cc0b1-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="cc0b1-174">Sprawdź możesz udostępniać komentarze i opinie NAS tutaj!</span><span class="sxs-lookup"><span data-stu-id="cc0b1-174">Please feel free to share comments or feedback with us here!</span></span>
