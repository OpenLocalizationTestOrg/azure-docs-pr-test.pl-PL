---
title: "Jak przeprowadzić migrację poszczególnych licencjonowanych użytkowników do grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak przejść z licencji użytkownika do grupy na podstawie licencji za pomocą usługi Azure Active Directory"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6b77dd4e9a6d361a05382397e89b575896fdad84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="ce3a8-104">Jak dodać licencjonowanych użytkowników do grupy licencji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce3a8-104">How to add licensed users to a group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="ce3a8-105">Masz istniejących licencji wdrożone dla użytkowników w organizacji za pomocą "przypisania bezpośredniego" oznacza to za pomocą skryptów programu PowerShell lub innych narzędzi, aby przypisać licencje do poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span></span> <span data-ttu-id="ce3a8-106">Jeśli chcesz rozpocząć korzystanie z zarządzanie licencjami w organizacji na podstawie grupy licencji, konieczne będzie planu migracji bezproblemowo zastąpić istniejące rozwiązania oparte na grupach licencji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="ce3a8-107">Ważne jest, należy wziąć pod uwagę to, że należy unikać sytuacji, w których migracja do licencjonowania na podstawie grupy spowoduje użytkownicy tymczasowo utraty ich aktualnie przypisane licencje.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="ce3a8-108">Aby usunąć ryzyko utraty dostępu do usług i ich danych należy unikać każdy proces, który może spowodować usunięcie licencji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="ce3a8-109">Proces migracji zalecane</span><span class="sxs-lookup"><span data-stu-id="ce3a8-109">Recommended migration process</span></span>

1. <span data-ttu-id="ce3a8-110">Masz istniejącej automatyzacji (na przykład programu PowerShell), zarządzanie przypisania licencji i usuwania dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="ce3a8-111">Usługa będzie działać, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-111">Leave it running as is.</span></span>

2. <span data-ttu-id="ce3a8-112">Utwórz nową grupę licencji (lub zdecydować, które istniejących grup do używania) i upewnij się, czy wszystkie wymagane użytkownicy zostaną dodane jako członkowie.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="ce3a8-113">Przypisywanie licencji wymagane do tych grup; Celem powinno być uwzględnienie tego samego stanu licencjonowania, które z istniejącej automatyzacji (na przykład programu PowerShell) jest stosowana do tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span></span>

4. <span data-ttu-id="ce3a8-114">Upewnij się, że licencje zostały zastosowane do wszystkich użytkowników w tych grupach.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-114">Verify that licenses have been applied to all users in those groups.</span></span> <span data-ttu-id="ce3a8-115">Można to zrobić, sprawdzając stan przetwarzania w każdej grupie oraz przez sprawdzanie dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-115">This can be done by checking the processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="ce3a8-116">Patrząc na ich szczegóły licencji można kontroli poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="ce3a8-117">Zobaczysz, że mają one taką samą licencji przypisanych "bezpośrednio" i "odziedziczony" z grupy.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="ce3a8-118">Można uruchomić skrypt programu PowerShell w celu [Sprawdź sposób przypisywania licencji do użytkowników](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span><span class="sxs-lookup"><span data-stu-id="ce3a8-118">You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="ce3a8-119">Tej samej licencji produktu jest przypisana do użytkownika zarówno bezpośrednio i za pośrednictwem grupy, tylko jedna licencja jest używane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span></span> <span data-ttu-id="ce3a8-120">Dlatego żadne dodatkowe licencje nie są wymagane do przeprowadzenia migracji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-120">Hence no additional licenses are required to perform migration.</span></span>

5. <span data-ttu-id="ce3a8-121">Upewnij się, że nie przypisań licencji nie sprawdzając każdej grupy użytkowników w stanie błędu.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="ce3a8-122">Aby uzyskać więcej informacji, zobacz [zidentyfikowanie i rozwiązywaniu problemów z licencji dla grupy](active-directory-licensing-group-problem-resolution-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce3a8-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="ce3a8-123">Rozważ usunięcie oryginalnego przypisania bezpośredniego; możesz zrobić to stopniowo etapami"", najpierw monitorowania wyników na podzestaw użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span></span>

  <span data-ttu-id="ce3a8-124">Można pozostawić oryginalny przypisania bezpośredniego na użytkowników, ale gdy użytkownicy opuszczają ich grup licencji, które zachowują nadal oryginalna licencja jest prawdopodobnie nie ma, które chcesz.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="ce3a8-125">Przykład</span><span class="sxs-lookup"><span data-stu-id="ce3a8-125">An example</span></span>

<span data-ttu-id="ce3a8-126">Mamy organizacji z 1000 użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="ce3a8-127">Wszyscy użytkownicy wymagają Enterprise Mobility + Security (EMS) licencji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="ce3a8-128">200 użytkowników są pracownikiem działu finansowego i wymagają licencji Office 365 Enterprise E3.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="ce3a8-129">Mamy uruchomiony lokalnie, dodawanie i usuwanie licencji od użytkowników, jak długo będą pochodzić i przejdź skryptów środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="ce3a8-130">Chcemy Zamień skryptu na podstawie grupy licencji, licencje są zarządzane automatycznie przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-130">We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="ce3a8-131">Oto, jak może wyglądać procesu migracji:</span><span class="sxs-lookup"><span data-stu-id="ce3a8-131">Here is what the migration process could look like:</span></span>

1. <span data-ttu-id="ce3a8-132">Przy użyciu portalu Azure przypisanie licencji pakietu EMS do **wszyscy użytkownicy** grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-132">Using the Azure portal assign the EMS license to the **All users** group in Azure AD.</span></span> <span data-ttu-id="ce3a8-133">Przypisywanie licencji E3 do **działu finansowego** grupy, która zawiera wszystkie wymagane użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span></span>

2. <span data-ttu-id="ce3a8-134">Dla każdej grupy upewnij się, że przypisanie licencji zostało zakończone dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="ce3a8-135">Przejdź do bloku dla każdej grupy, wybierz opcję **licencji**i sprawdź stan przetwarzania w górnej części **licencji** bloku.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span></span>

  - <span data-ttu-id="ce3a8-136">Wyszukaj "Licencji najnowsze zmiany zostały zastosowane do wszystkich użytkowników" Aby upewnić się, przetwarzanie zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span></span>

  - <span data-ttu-id="ce3a8-137">Poszukaj powiadomienia w górnej części o wszyscy użytkownicy, dla których licencji mogą nie zostały pomyślnie przypisane.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="ce3a8-138">Czy możemy zabraknie licencji dla niektórych użytkowników?</span><span class="sxs-lookup"><span data-stu-id="ce3a8-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="ce3a8-139">W przypadku niektórych użytkowników, czy mają powodujące konflikt licencji jednostki magazynowe, które uniemożliwiają dziedziczenie grupy licencji?</span><span class="sxs-lookup"><span data-stu-id="ce3a8-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="ce3a8-140">Miejsce Sprawdź niektórych użytkowników, aby sprawdzić, czy mają one zarówno bezpośrednie i grup licencji zastosowane.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-140">Spot check some users to verify that they have both the direct and group licenses applied.</span></span> <span data-ttu-id="ce3a8-141">Przejdź do bloku dla użytkownika, zaznacz **licencji**i sprawdź, czy stan licencji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span></span>

  - <span data-ttu-id="ce3a8-142">Jest to stan oczekiwany użytkownika podczas migracji:</span><span class="sxs-lookup"><span data-stu-id="ce3a8-142">This is the expected user state during migration:</span></span>

      ![Stan użytkownika oczekiwany](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="ce3a8-144">Potwierdza to, czy użytkownik ma licencje zarówno bezpośrednio, jak i dziedziczone.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-144">This confirms that the user has both direct and inherited licenses.</span></span> <span data-ttu-id="ce3a8-145">Firma Microsoft wyświetlana zarówno **EMS** i **E3** są przypisane.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="ce3a8-146">Wybierz każdej licencji, aby wyświetlić szczegółowe informacje o włączone usługi.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-146">Select each license to show details about the enabled services.</span></span> <span data-ttu-id="ce3a8-147">Może to służyć do Sprawdź dokładnie tego samego planów usługi dla użytkownika włączyć bezpośredniego i grup licencji.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span></span>

      ![Sprawdź planów usługi](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="ce3a8-149">Po potwierdzeniu, że zarówno bezpośrednio, jak i grupy licencji są równoważne, można uruchomić, usunięcie licencji bezpośrednio od użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="ce3a8-150">Można to sprawdzić, usuwając je dla poszczególnych użytkowników w portalu, a następnie uruchom skryptów automatyzacji je usunąć zbiorczo.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span></span> <span data-ttu-id="ce3a8-151">Oto przykład tego samego użytkownika z licencjami bezpośredniego usunięte za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-151">Here is an example of the same user with the direct licenses removed through the portal.</span></span> <span data-ttu-id="ce3a8-152">Zwróć uwagę, stan licencji nie jest zmieniany, że firma Microsoft nie jest już wyświetlana bezpośredniego przypisania.</span><span class="sxs-lookup"><span data-stu-id="ce3a8-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![bezpośrednie licencje usunięte](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="ce3a8-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce3a8-154">Next steps</span></span>

<span data-ttu-id="ce3a8-155">Aby dowiedzieć się więcej na temat innych scenariuszy zarządzania licencji za pomocą grup, do odczytu</span><span class="sxs-lookup"><span data-stu-id="ce3a8-155">To learn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="ce3a8-156">Przypisywanie licencji do grupy w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce3a8-156">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="ce3a8-157">Co to jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce3a8-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="ce3a8-158">Identyfikowanie i rozwiązywanie problemów z licencji dla grupy w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce3a8-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="ce3a8-159">Usługa Azure Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="ce3a8-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
