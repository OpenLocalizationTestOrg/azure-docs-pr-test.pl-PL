---
title: "aaaAzure Privileged Identity Management przepływów pracy | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="4b3f6-103">Zatwierdzenia (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="4b3f6-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="4b3f6-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4b3f6-104">Overview</span></span>

<span data-ttu-id="4b3f6-105">Z zatwierdzenia Privileged Identity Management można skonfigurować role toorequire zatwierdzenia dla aktywacji i wybrać jednego lub wielu użytkowników lub grup tak delegowani osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="4b3f6-106">Zachowaj jak odczytywania toolearn tooconfigure ról i wybierz osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="4b3f6-107">Pamiętaj, ta funkcja jest nadal w rozwoju i mogą wystąpić błędy.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="4b3f6-108">Funkcje Hello, łącznie z tekstem i konwencje nazewnictwa mogą ulec zmianie, a nie należy traktować jako ostatecznego.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="4b3f6-109">Kluczową terminologię</span><span class="sxs-lookup"><span data-stu-id="4b3f6-109">Key Terminology</span></span>

<span data-ttu-id="4b3f6-110">*Kwalifikujące się roli użytkownika* — kwalifikujących się roli użytkownik jest użytkownikiem w organizacji, któremu przypisano rolę tooan usługi Azure AD jako uprawniających (rola wymaga aktywacji).</span><span class="sxs-lookup"><span data-stu-id="4b3f6-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="4b3f6-111">*Delegowane osoba zatwierdzająca* — delegowanego osoba zatwierdzająca jest jednego lub wielu osób lub grup w ramach usługi Azure AD, odpowiedzialnych za zatwierdzanie żądań dla roli aktywacji.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="4b3f6-112">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="4b3f6-112">Scenarios</span></span>

<span data-ttu-id="4b3f6-113">Witaj prywatnej wersji zapoznawczej obsługuje hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="4b3f6-114">**Jako uprzywilejowane roli administratora pararozaniliny można wykonywać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4b3f6-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="4b3f6-115">Włącz zatwierdzenia dla określonych ról</span><span class="sxs-lookup"><span data-stu-id="4b3f6-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="4b3f6-116">Określ żądań tooapprove osoba zatwierdzająca użytkowników i/lub grup</span><span class="sxs-lookup"><span data-stu-id="4b3f6-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="4b3f6-117">Wyświetl historię żądań i zatwierdzania dla wszystkich ról uprzywilejowanych</span><span class="sxs-lookup"><span data-stu-id="4b3f6-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="4b3f6-118">**Wyznaczone osoby zatwierdzającej można:**</span><span class="sxs-lookup"><span data-stu-id="4b3f6-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="4b3f6-119">Wyświetlanie oczekujących zatwierdzeń (liczba żądań)</span><span class="sxs-lookup"><span data-stu-id="4b3f6-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="4b3f6-120">Zatwierdzanie lub odrzucanie żądań w celu podniesienia roli (pojedynczego i/lub masowo)</span><span class="sxs-lookup"><span data-stu-id="4b3f6-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="4b3f6-121">Podaj uzasadnienie dla moich lub odrzuceniu</span><span class="sxs-lookup"><span data-stu-id="4b3f6-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="4b3f6-122">**Kwalifikujące się roli użytkownika może:**</span><span class="sxs-lookup"><span data-stu-id="4b3f6-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="4b3f6-123">żądanie aktywacji roli, która wymaga zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="4b3f6-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="4b3f6-124">Wyświetlanie stanu hello tooactivate Twojego żądania</span><span class="sxs-lookup"><span data-stu-id="4b3f6-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="4b3f6-125">wykonać zadanie w usłudze Azure AD, jeśli Aktywacja została zatwierdzona</span><span class="sxs-lookup"><span data-stu-id="4b3f6-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="4b3f6-126">Nawigacji</span><span class="sxs-lookup"><span data-stu-id="4b3f6-126">Navigation</span></span>

<span data-ttu-id="4b3f6-127">Zaktualizowaliśmy hello nawigacji toosupport zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="4b3f6-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="4b3f6-128">Witaj domyślna strona docelowa zawiera tooinformation najwygodniejszy dostęp o PIM i hello Nowa dokumentacja zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="4b3f6-129">Dodaliśmy również nową sekcję dla wszystkich użytkowników PIM, "Moje Historia inspekcji".</span><span class="sxs-lookup"><span data-stu-id="4b3f6-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="4b3f6-130">W tym miejscu można znaleźć wszystkie hello informacje istotne tooyour tożsamości.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="4b3f6-131">W tym wszystkie swoje żądania oczekujące i ukończone, wszelkich decyzji, których dokonano hello żądań, które należy rozwiązać i wszystkich poprzednich aktywacji roli w jednej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="4b3f6-132">Włącz zatwierdzenia dla określonych ról</span><span class="sxs-lookup"><span data-stu-id="4b3f6-132">Enable approval for specific roles</span></span>

<span data-ttu-id="4b3f6-133">tooenable zatwierdzenia dla konkretnej roli, najpierw wybierz role katalogu z hello nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="4b3f6-134">Znajdź i wybierz ustawienia w hello nawigacji po lewej stronie ról katalogu</span><span class="sxs-lookup"><span data-stu-id="4b3f6-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="4b3f6-135">Wybierz role uprzywilejowane:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="4b3f6-136">Zaznacz pole wyboru "Włącz" w hello wymagają zatwierdzenia sekcji:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="4b3f6-137">Po włączeniu bloku hello rozwinie hello tooshow poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="4b3f6-138">Jeśli nie określono żadnych osób zatwierdzających, hello PRA(s) stają się osoby zatwierdzające domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="4b3f6-139">PRA(s) może być wymagane tooapprove aktywacji wszystkie żądania dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="4b3f6-140">Określ żądań tooapprove osoba zatwierdzająca użytkowników i/lub grup</span><span class="sxs-lookup"><span data-stu-id="4b3f6-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="4b3f6-141">zatwierdzenie toodelegate, kliknij opcję hello zbyt "Wybierz osób zatwierdzających":</span><span class="sxs-lookup"><span data-stu-id="4b3f6-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="4b3f6-142">Podczas ładowania bloku wybierz osób zatwierdzających hello może wyszukać określonego użytkownika lub grupy za pomocą hello pasek wyszukiwania w górnej hello lub wybrać z listy wstępnie wypełnione hello, a następnie kliknij "Wybierz" po zakończeniu:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="4b3f6-143">Uwaga: Można wybrać wielu użytkowników lub grup w czasie.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="4b3f6-144">Wybór pojawi się w wybranej listy hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="4b3f6-145">tooremove osoba zatwierdzająca, wystarczy kliknąć hello Usuń przycisku Dalej tootheir nazwę.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="4b3f6-146">tooadd dodatkowe osób zatwierdzających, proces hello powtarzania.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="4b3f6-147">Wyświetl historię żądań i zatwierdzania dla wszystkich ról uprzywilejowanych</span><span class="sxs-lookup"><span data-stu-id="4b3f6-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="4b3f6-148">Historia żądania i zatwierdzania tooview dla wszystkich ról uprzywilejowanych, wybierz Historia inspekcji z pulpitu nawigacyjnego hello:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="4b3f6-149">Sortowanie danych hello przez akcję i wyszukaj "Zatwierdzone aktywacji"</span><span class="sxs-lookup"><span data-stu-id="4b3f6-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="4b3f6-150">Wyświetlanie oczekujących zatwierdzeń (liczba żądań)</span><span class="sxs-lookup"><span data-stu-id="4b3f6-150">View pending approvals (requests)</span></span>

<span data-ttu-id="4b3f6-151">Zatwierdzającą delegowanego będzie otrzymywał powiadomienia e-mail, kiedy żądanie oczekuje na zatwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="4b3f6-152">tooview te żądania w portalu usługi PIM hello, na karcie Wybierz hello "oczekujących żądań zatwierdzenia" Pulpit nawigacyjny (w nawigacji nowe hello) w hello lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="4b3f6-153">Z tego miejsca zobaczysz listę żądania w oczekiwaniu na zatwierdzenie:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="4b3f6-154">Zatwierdzanie lub odrzucanie żądań w celu podniesienia roli (pojedynczego i/lub masowo)</span><span class="sxs-lookup"><span data-stu-id="4b3f6-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="4b3f6-155">Wybierz hello żądania ma tooapprove lub odmowy i kliknij przycisk hello w pasku akcji, który odpowiada decyzji:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="4b3f6-156">Podaj uzasadnienie dla moich lub odrzuceniu</span><span class="sxs-lookup"><span data-stu-id="4b3f6-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="4b3f6-157">Będzie to Otwórz nowe tooapprove bloku lub odrzucanie jednocześnie wiele żądań.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="4b3f6-158">Wprowadź uzasadnienie decyzji, i kliknij przycisk Zatwierdź (lub Odmów) hello lub bloku hello:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="4b3f6-159">Po zakończeniu procesu żądania hello hello symbolu stanu będzie odzwierciedlać wprowadzone decyzji (w tym przykładzie decyzji hello jest zatwierdzić):</span><span class="sxs-lookup"><span data-stu-id="4b3f6-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="4b3f6-160">Żądania aktywacji roli, która wymaga zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="4b3f6-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="4b3f6-161">Żądanie aktywacji roli, który wymaga zatwierdzenia można zainicjować z hello starego PIM nawigacji lub hello nowe nawigacji, jako proces hello roli aktywacji pozostaje hello takie same.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="4b3f6-162">Po prostu wybierz rolę z listy hello ról do aktywacji:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="4b3f6-163">Jeśli ról uprzywilejowanych wymaga uwierzytelniania wieloskładnikowego, zostanie wyświetlony monit przeprowadzenie tego zadania:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="4b3f6-164">Po jego zakończeniu, kliknij przycisk Aktywuj i uzasadnić (jeśli jest to wymagane):</span><span class="sxs-lookup"><span data-stu-id="4b3f6-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="4b3f6-165">obiektu żądającego Hello pojawią się, że powiadomienie, które hello żądania oczekuje na zatwierdzenie:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="4b3f6-166">Wyświetlanie stanu hello tooactivate Twojego żądania</span><span class="sxs-lookup"><span data-stu-id="4b3f6-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="4b3f6-167">Wyświetlanie stanu hello tooactivate oczekujące żądania musi być dostępny z nowego nawigacji.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="4b3f6-168">Z hello paska nawigacji po lewej stronie wybierz kartę "Moje żądania" hello:</span><span class="sxs-lookup"><span data-stu-id="4b3f6-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="4b3f6-169">Stan żądania Hello zbyt domyślne "Oczekujące", ale może przełączyć toosee wszystkie lub odrzucone żądania.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="4b3f6-170">Wykonać zadanie w usłudze Azure AD, jeśli Aktywacja została zatwierdzona</span><span class="sxs-lookup"><span data-stu-id="4b3f6-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="4b3f6-171">Po zatwierdzeniu żądania hello rola hello jest aktywna i może kontynuować pracę, która wymaga tej roli.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="4b3f6-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4b3f6-172">Next steps</span></span>

<span data-ttu-id="4b3f6-173">Twoja opinia jest przydatna toous.</span><span class="sxs-lookup"><span data-stu-id="4b3f6-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="4b3f6-174">Wyślij komentarze wolnego tooshare lub opinii z nami tutaj!</span><span class="sxs-lookup"><span data-stu-id="4b3f6-174">Please feel free tooshare comments or feedback with us here!</span></span>
