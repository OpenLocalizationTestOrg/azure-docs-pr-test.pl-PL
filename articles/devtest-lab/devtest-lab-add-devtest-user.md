---
title: "aaaAdd właścicieli i użytkowników w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs przy użyciu hello portalu Azure lub programu PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="89900-103">Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="89900-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="89900-104">Steruje dostępu w usłudze Azure DevTest Labs [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="89900-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="89900-105">Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji do *ról* gdzie udzielić tylko hello ilość tooperform niezbędne toousers dostęp do swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="89900-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="89900-106">Są trzy te role RBAC *właściciela*, *DevTest Labs użytkownika*, i *współautora*.</span><span class="sxs-lookup"><span data-stu-id="89900-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="89900-107">W tym artykule dowiesz się, jakie akcje można wykonać w każdym trzy główne role RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="89900-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="89900-108">Z tego miejsca, możesz dowiedzieć się, jak laboratorium tooa użytkowników tooadd — zarówno za pośrednictwem hello portalu i za pomocą skryptu programu PowerShell i jak użytkownicy tooadd hello poziomu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="89900-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="89900-109">Akcje, które mogą być wykonywane w każdej roli</span><span class="sxs-lookup"><span data-stu-id="89900-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="89900-110">Istnieją trzy główne role przypisanie użytkownika:</span><span class="sxs-lookup"><span data-stu-id="89900-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="89900-111">Właściciel</span><span class="sxs-lookup"><span data-stu-id="89900-111">Owner</span></span>
* <span data-ttu-id="89900-112">DevTest Labs użytkownika</span><span class="sxs-lookup"><span data-stu-id="89900-112">DevTest Labs User</span></span>
* <span data-ttu-id="89900-113">Współautor</span><span class="sxs-lookup"><span data-stu-id="89900-113">Contributor</span></span>

<span data-ttu-id="89900-114">Witaj poniższej tabeli przedstawiono akcje hello, które mogą być wykonywane przez użytkowników w każdej z tych ról:</span><span class="sxs-lookup"><span data-stu-id="89900-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="89900-115">**Można wykonać akcje użytkowników w tej roli**</span><span class="sxs-lookup"><span data-stu-id="89900-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="89900-116">**DevTest Labs użytkownika**</span><span class="sxs-lookup"><span data-stu-id="89900-116">**DevTest Labs User**</span></span> | <span data-ttu-id="89900-117">**Właściciel**</span><span class="sxs-lookup"><span data-stu-id="89900-117">**Owner**</span></span> | <span data-ttu-id="89900-118">**Współautora**</span><span class="sxs-lookup"><span data-stu-id="89900-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89900-119">**Zadania laboratorium**</span><span class="sxs-lookup"><span data-stu-id="89900-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="89900-120">Dodaj użytkowników tooa laboratorium</span><span class="sxs-lookup"><span data-stu-id="89900-120">Add users tooa lab</span></span> |<span data-ttu-id="89900-121">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-121">No</span></span> |<span data-ttu-id="89900-122">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-122">Yes</span></span> |<span data-ttu-id="89900-123">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-123">No</span></span> |
| <span data-ttu-id="89900-124">Aktualizowanie ustawień koszt</span><span class="sxs-lookup"><span data-stu-id="89900-124">Update cost settings</span></span> |<span data-ttu-id="89900-125">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-125">No</span></span> |<span data-ttu-id="89900-126">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-126">Yes</span></span> |<span data-ttu-id="89900-127">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-127">Yes</span></span> |
| <span data-ttu-id="89900-128">**Zadania podstawowej maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="89900-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="89900-129">Dodawanie i usuwanie niestandardowych obrazów</span><span class="sxs-lookup"><span data-stu-id="89900-129">Add and remove custom images</span></span> |<span data-ttu-id="89900-130">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-130">No</span></span> |<span data-ttu-id="89900-131">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-131">Yes</span></span> |<span data-ttu-id="89900-132">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-132">Yes</span></span> |
| <span data-ttu-id="89900-133">Dodawanie, aktualizowanie i usuwanie formuły</span><span class="sxs-lookup"><span data-stu-id="89900-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="89900-134">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-134">Yes</span></span> |<span data-ttu-id="89900-135">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-135">Yes</span></span> |<span data-ttu-id="89900-136">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-136">Yes</span></span> |
| <span data-ttu-id="89900-137">Obrazy dozwolonych Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="89900-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="89900-138">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-138">No</span></span> |<span data-ttu-id="89900-139">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-139">Yes</span></span> |<span data-ttu-id="89900-140">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-140">Yes</span></span> |
| <span data-ttu-id="89900-141">**Zadania maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="89900-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="89900-142">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="89900-142">Create VMs</span></span> |<span data-ttu-id="89900-143">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-143">Yes</span></span> |<span data-ttu-id="89900-144">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-144">Yes</span></span> |<span data-ttu-id="89900-145">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-145">Yes</span></span> |
| <span data-ttu-id="89900-146">Uruchamianie, zatrzymywanie i usuwanie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="89900-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="89900-147">Tylko maszyny wirtualne utworzone przez użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="89900-147">Only VMs created by hello user</span></span> |<span data-ttu-id="89900-148">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-148">Yes</span></span> |<span data-ttu-id="89900-149">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-149">Yes</span></span> |
| <span data-ttu-id="89900-150">Aktualizowanie zasad maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89900-150">Update VM policies</span></span> |<span data-ttu-id="89900-151">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-151">No</span></span> |<span data-ttu-id="89900-152">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-152">Yes</span></span> |<span data-ttu-id="89900-153">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-153">Yes</span></span> |
| <span data-ttu-id="89900-154">Dodawanie/usuwanie dysków z danymi z maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="89900-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="89900-155">Tylko maszyny wirtualne utworzone przez użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="89900-155">Only VMs created by hello user</span></span> |<span data-ttu-id="89900-156">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-156">Yes</span></span> |<span data-ttu-id="89900-157">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-157">Yes</span></span> |
| <span data-ttu-id="89900-158">**Zadania artefaktów**</span><span class="sxs-lookup"><span data-stu-id="89900-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="89900-159">Dodawanie i usuwanie repozytoria artefaktów</span><span class="sxs-lookup"><span data-stu-id="89900-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="89900-160">Nie</span><span class="sxs-lookup"><span data-stu-id="89900-160">No</span></span> |<span data-ttu-id="89900-161">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-161">Yes</span></span> |<span data-ttu-id="89900-162">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-162">Yes</span></span> |
| <span data-ttu-id="89900-163">Zastosuj artefaktów</span><span class="sxs-lookup"><span data-stu-id="89900-163">Apply artifacts</span></span> |<span data-ttu-id="89900-164">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-164">Yes</span></span> |<span data-ttu-id="89900-165">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-165">Yes</span></span> |<span data-ttu-id="89900-166">Tak</span><span class="sxs-lookup"><span data-stu-id="89900-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="89900-167">Gdy użytkownik tworzy Maszynę wirtualną, ten użytkownik zostanie automatycznie przypisany toohello **właściciela** roli hello utworzyć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89900-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="89900-168">Dodawanie właściciela lub użytkownika na poziomie laboratorium hello</span><span class="sxs-lookup"><span data-stu-id="89900-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="89900-169">Na poziomie laboratorium hello za pośrednictwem portalu Azure hello można dodać właścicieli i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="89900-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="89900-170">Dotyczy to również użytkowników zewnętrznych z prawidłowym [konta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="89900-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="89900-171">następujące kroki Hello informacje pomocne przy hello proces dodawania laboratorium tooa właściciela lub użytkowników w usłudze Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="89900-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="89900-172">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="89900-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="89900-173">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="89900-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="89900-174">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="89900-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="89900-175">W bloku hello laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="89900-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="89900-176">Na powitania **konfiguracji** bloku, wybierz opcję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="89900-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="89900-177">Na powitania **użytkowników** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="89900-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Dodawanie użytkownika](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="89900-179">Na powitania **wybierz rolę** bloku, hello wybierz odpowiednią rolę.</span><span class="sxs-lookup"><span data-stu-id="89900-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="89900-180">Witaj sekcji [akcje, które mogą być wykonywane w każdej roli](#actions-that-can-be-performed-in-each-role) list hello różne akcje, które mogą być wykonywane przez użytkowników pełniących role hello właściciela, DevTest użytkownika i współautor.</span><span class="sxs-lookup"><span data-stu-id="89900-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="89900-181">Na powitania **dodawania użytkowników** bloku, wprowadź adres e-mail hello lub nazwa użytkownika hello ma tooadd w określonej roli hello.</span><span class="sxs-lookup"><span data-stu-id="89900-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="89900-182">Jeśli nie można odnaleźć użytkownika hello, komunikat o błędzie wyjaśniono hello problem.</span><span class="sxs-lookup"><span data-stu-id="89900-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="89900-183">Jeśli użytkownik hello zostanie znaleziony, ten użytkownik jest na liście i wybrać.</span><span class="sxs-lookup"><span data-stu-id="89900-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="89900-184">Wybierz **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="89900-184">Select **Select**.</span></span>
10. <span data-ttu-id="89900-185">Wybierz **OK** tooclose hello **Dodawanie dostępu** bloku.</span><span class="sxs-lookup"><span data-stu-id="89900-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="89900-186">Po powrocie toohello **użytkowników** bloku hello użytkownik został dodany.</span><span class="sxs-lookup"><span data-stu-id="89900-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="89900-187">Dodaj użytkownika zewnętrznego laboratorium tooa przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="89900-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="89900-188">Ponadto tooadding użytkowników w portalu Azure hello, można dodać użytkownika zewnętrznego laboratorium tooyour za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89900-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="89900-189">W hello poniższy przykład, wystarczy zmodyfikować hello wartości parametrów w obszarze hello **toochange wartości** komentarza.</span><span class="sxs-lookup"><span data-stu-id="89900-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="89900-190">Możesz pobrać hello `subscriptionId`, `labResourceGroup`, i `labName` wartości z bloku laboratorium hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="89900-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="89900-191">Witaj przykładowy skrypt przyjęto założenie, że tego hello określony użytkownik został dodany jako gość toohello usługi Active Directory i zakończy się niepowodzeniem, jeśli nie jest ona hello przypadku.</span><span class="sxs-lookup"><span data-stu-id="89900-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="89900-192">tooadd użytkownik nie istnieje w hello laboratorium tooa usługi Active Directory, użyj roli użytkownika hello hello tooassign portalu Azure w tooa, jak pokazano w sekcji hello [dodać właściciela lub użytkownika na poziomie laboratorium hello](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="89900-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="89900-193">Dodawanie właściciela lub użytkowników na poziomie subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="89900-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="89900-194">Azure uprawnienia zostały przeniesione z zakresu toochild zakresu nadrzędnego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="89900-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="89900-195">W związku z tym właściciele subskrypcji platformy Azure, która zawiera labs są automatycznie właścicieli tych labs.</span><span class="sxs-lookup"><span data-stu-id="89900-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="89900-196">Właścicielem również hello maszyn wirtualnych i innych zasobów tworzone przez użytkowników hello laboratorium i hello Azure DevTest Labs usługi.</span><span class="sxs-lookup"><span data-stu-id="89900-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="89900-197">Można dodać dodatkowe właścicieli laboratorium tooa za pomocą bloku laboratorium hello hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="89900-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="89900-198">Jednak hello dodano zakres właściciela administracji jest coraz węższego niż właściciel subskrypcji hello zakresu.</span><span class="sxs-lookup"><span data-stu-id="89900-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="89900-199">Na przykład hello dodać właścicieli nie mają pełny dostęp toosome hello zasobów, które są tworzone w ramach subskrypcji hello przez hello usługi DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="89900-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="89900-200">tooadd tooan właściciela subskrypcji platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="89900-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="89900-201">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="89900-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="89900-202">Wybierz **więcej usług**, a następnie wybierz **subskrypcje** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="89900-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="89900-203">Wybierz żądaną hello subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="89900-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="89900-204">Wybierz **dostępu** ikony.</span><span class="sxs-lookup"><span data-stu-id="89900-204">Select **Access** icon.</span></span> 
   
    ![Dostęp do użytkowników](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="89900-206">Na powitania **użytkowników** bloku, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="89900-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Dodawanie użytkownika](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="89900-208">Na powitania **wybierz rolę** bloku, wybierz **właściciela**.</span><span class="sxs-lookup"><span data-stu-id="89900-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="89900-209">Na powitania **dodawania użytkowników** bloku, wprowadź adres e-mail hello lub nazwa użytkownika hello ma tooadd jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="89900-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="89900-210">Jeśli nie można odnaleźć użytkownika hello, otrzymasz komunikat o błędzie wyjaśniający hello problem.</span><span class="sxs-lookup"><span data-stu-id="89900-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="89900-211">Jeśli użytkownik hello zostanie znaleziony, ten użytkownik zostanie wyświetlony w obszarze hello **użytkownika** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="89900-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="89900-212">Wybierz nazwę użytkownika znajduje się hello.</span><span class="sxs-lookup"><span data-stu-id="89900-212">Select hello located user name.</span></span>
9. <span data-ttu-id="89900-213">Wybierz **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="89900-213">Select **Select**.</span></span>
10. <span data-ttu-id="89900-214">Wybierz **OK** tooclose hello **Dodawanie dostępu** bloku.</span><span class="sxs-lookup"><span data-stu-id="89900-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="89900-215">Po powrocie toohello **użytkowników** bloku hello użytkownik został dodany jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="89900-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="89900-216">Ten użytkownik jest obecnie właścicielem żadnych labs utworzone w ramach tej subskrypcji, a w związku z tym być stanie tooperform właściciela zadania.</span><span class="sxs-lookup"><span data-stu-id="89900-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

