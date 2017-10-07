---
title: "aaaAdd Azure automatyzacji elementów runbook toorecovery plany w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługi Azure Site Recovery można rozszerzyć planów odzyskiwania przy użyciu usługi Automatyzacja Azure. Dowiedz się, jak toocomplete złożone zadania podczas tooAzure odzyskiwania."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="ec9e5-104">Dodaj planów toorecovery elementów runbook usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="ec9e5-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="ec9e5-105">W tym artykule opisano sposób Azure Site Recovery integruje się z usługi Automatyzacja Azure toohelp rozszerzyć planów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="ec9e5-106">Plany odzyskiwania można organizować odzyskiwania maszyn wirtualnych, które są chronione za pomocą usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="ec9e5-107">Plany odzyskiwania działa zarówno dla chmury dodatkowej tooa replikacji i tooAzure replikacji.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="ec9e5-108">Plany odzyskiwania również sprawić, że odzyskiwania hello **spójnie dokładne**, **powtarzalne**, i **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="ec9e5-109">Jeśli nie zostanie za pośrednictwem sieci tooAzure maszyn wirtualnych, integracja z usługi Automatyzacja Azure rozszerza planów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="ec9e5-110">Służy on tooexecute elementów runbook, które oferują zaawansowane automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="ec9e5-111">W przypadku nowych tooAzure automatyzacji może [Zarejestruj](https://azure.microsoft.com/services/automation/) i [Pobierz przykładowe skrypty](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="ec9e5-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="ec9e5-112">Aby uzyskać więcej informacji i toolearn jak tooorchestrate tooAzure odzyskiwania przy użyciu [planów odzyskiwania](https://azure.microsoft.com/blog/?p=166264), zobacz [usługi Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="ec9e5-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="ec9e5-113">W tym artykule opisano sposób integrowania elementu runbook usługi Automatyzacja Azure do planów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="ec9e5-114">Używamy przykłady tooautomate podstawowe zadania, które wcześniej wymagały ręcznej interwencji.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="ec9e5-115">Opisano również sposób tooconvert tooa odzyskiwania wieloetapowych jednym kliknięciem Akcja odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="ec9e5-116">Dostosowywanie hello planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ec9e5-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="ec9e5-117">Przejdź toohello **usługi Site Recovery** bloku zasobów planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="ec9e5-118">Na przykład hello plan odzyskiwania obejmuje dwa tooit dodano maszyn wirtualnych, do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="ec9e5-119">toobegin Dodawanie elementu runbook, kliknij przycisk hello **Dostosuj** kartę.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Kliknij przycisk Dostosuj hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="ec9e5-121">Kliknij prawym przyciskiem myszy **Grupa 1: Uruchom**, a następnie wybierz **post dodać akcję**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Kliknij prawym przyciskiem myszy Grupa 1: Uruchom i dodać post akcji](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="ec9e5-123">Kliknij przycisk **wybierz skrypt**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="ec9e5-124">Na powitania **Akcja aktualizacji** bloku, nazwa skryptu hello **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![Witaj aktualizacji akcji bloku](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="ec9e5-126">Wprowadź nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="ec9e5-127">Konto automatyzacji Hello można w dowolnym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="ec9e5-128">Hello konta automatyzacji musi należeć do hello tej samej subskrypcji co magazyn usługi Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="ec9e5-129">Na Twoim koncie automatyzacji wybierz element runbook.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="ec9e5-130">Ten element runbook jest hello skrypt, który jest uruchamiany podczas wykonywania hello hello planu odzyskiwania, po odzyskaniu hello hello pierwszej grupy.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="ec9e5-131">skrypt hello toosave, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="ec9e5-132">skrypt Hello jest dodawany zbyt**Grupa 1: kroki po**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![1:Start grupy po akcji](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="ec9e5-134">Zagadnienia dotyczące Dodawanie skryptu</span><span class="sxs-lookup"><span data-stu-id="ec9e5-134">Considerations for adding a script</span></span>

* <span data-ttu-id="ec9e5-135">Dla opcji zbyt**usunąć krok** lub **hello skrypt aktualizacji**, kliknij prawym przyciskiem myszy hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="ec9e5-136">Skrypt można uruchomić na platformie Azure w trybie failover z tooAzure komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="ec9e5-137">Ponadto można go uruchomić na platformie Azure jako skrypt lokacji podstawowej zamknięcia systemu, podczas powrotu po awarii z platformy Azure tooan na lokalnej maszynie.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="ec9e5-138">Po uruchomieniu skryptu injects kontekstu planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="ec9e5-139">Witaj poniższy przykład przedstawia zmiennej kontekstu:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="ec9e5-140">Witaj w poniższej tabeli wymieniono hello nazwę i opis każdej zmiennej w kontekście hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="ec9e5-141">**Nazwa zmiennej**</span><span class="sxs-lookup"><span data-stu-id="ec9e5-141">**Variable name**</span></span> | <span data-ttu-id="ec9e5-142">**Opis**</span><span class="sxs-lookup"><span data-stu-id="ec9e5-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="ec9e5-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="ec9e5-143">RecoveryPlanName</span></span> |<span data-ttu-id="ec9e5-144">Nazwa Hello planu hello uruchomione.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-144">hello name of hello plan being run.</span></span> <span data-ttu-id="ec9e5-145">Ta zmienna pomaga wykonać różne operacje, na podstawie nazwy planu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="ec9e5-146">Również można ponownie użyć skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="ec9e5-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="ec9e5-147">FailoverType</span></span> |<span data-ttu-id="ec9e5-148">Określa, czy tryb failover hello testu, planowane lub nieplanowane.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="ec9e5-149">Element FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="ec9e5-149">FailoverDirection</span></span> |<span data-ttu-id="ec9e5-150">Określa, czy odzyskiwania tooa podstawowej lub dodatkowej lokacji.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="ec9e5-151">Identyfikator grupy</span><span class="sxs-lookup"><span data-stu-id="ec9e5-151">GroupID</span></span> |<span data-ttu-id="ec9e5-152">Identyfikuje numer grupy hello w planie odzyskiwania hello uruchomionej hello planu.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="ec9e5-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="ec9e5-153">VmMap</span></span> |<span data-ttu-id="ec9e5-154">Tablica wszystkich maszyn wirtualnych w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="ec9e5-155">Klucz VMMap</span><span class="sxs-lookup"><span data-stu-id="ec9e5-155">VMMap key</span></span> |<span data-ttu-id="ec9e5-156">Unikatowy klucz (GUID) dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="ec9e5-157">Witaj sam jak identyfikator Azure Virtual Machine Manager (VMM) hello hello maszyny Wirtualnej, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="ec9e5-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ec9e5-158">SubscriptionId</span></span> |<span data-ttu-id="ec9e5-159">Identyfikator subskrypcji platformy Azure Hello, w których hello maszyna wirtualna została utworzona.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="ec9e5-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="ec9e5-160">RoleName</span></span> |<span data-ttu-id="ec9e5-161">Nazwa Hello hello maszyny Wirtualnej platformy Azure, która jest przywracana.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="ec9e5-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="ec9e5-162">CloudServiceName</span></span> |<span data-ttu-id="ec9e5-163">Nazwa usługi w chmurze Azure Hello pod które hello maszyna wirtualna została utworzona.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="ec9e5-164">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="ec9e5-164">ResourceGroupName</span></span>|<span data-ttu-id="ec9e5-165">Nazwa grupy zasobów platformy Azure Hello pod którą hello maszyna wirtualna została utworzona.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="ec9e5-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="ec9e5-166">RecoveryPointId</span></span>|<span data-ttu-id="ec9e5-167">Witaj sygnaturę czasową po odzyskaniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="ec9e5-168">Upewnij się, że tego konta automatyzacji hello ma hello następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="ec9e5-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="ec9e5-169">AzureRM.profile</span></span>
    * <span data-ttu-id="ec9e5-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="ec9e5-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="ec9e5-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="ec9e5-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="ec9e5-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="ec9e5-172">AzureRM.Network</span></span>
    * <span data-ttu-id="ec9e5-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="ec9e5-173">AzureRM.Compute</span></span>

<span data-ttu-id="ec9e5-174">Wszystkie moduły muszą być zgodne wersje.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="ec9e5-175">Tooensure łatwy sposób, że wszystkie moduły są zgodne jest toouse hello najnowsze wersje wszystkich modułów hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="ec9e5-176">Dostęp do wszystkich maszyn wirtualnych z hello VMMap w pętli</span><span class="sxs-lookup"><span data-stu-id="ec9e5-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="ec9e5-177">Użyj następującego kodu tooloop na wszystkich maszynach wirtualnych z hello Microsoft VMMap hello:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="ec9e5-178">Hello grupy nazwa i rola Nazwa wartości zasobów są puste, gdy skrypt hello jest grupy rozruchu tooa akcji przed.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="ec9e5-179">wartości Hello są wypełniane tylko wtedy, gdy hello maszyn wirtualnych w danej grupie powiedzie się w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="ec9e5-180">skrypt Hello jest akcją po hello grupy rozruchu.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="ec9e5-181">Użyj hello sam element runbook automatyzacji w wielu planów odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ec9e5-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="ec9e5-182">Możesz użyć jednego skryptu w wielu planów odzyskiwania za pomocą zmiennych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="ec9e5-183">Można użyć [zmienne automatyzacji Azure](../automation/automation-variables.md) toostore parametrów, które można przekazać do odzyskiwania planu wykonania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="ec9e5-184">Dodając Nazwa planu odzyskiwania hello jako zmienną toohello prefiksu, można utworzyć pojedyncze zmienne dla każdego planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="ec9e5-185">Następnie należy użyć zmiennych hello jako parametry.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="ec9e5-186">Bez zmieniania hello skryptu można zmienić parametru, ale nadal hello zmiany hello sposób działania skryptu.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="ec9e5-187">Użyj zmiennej prostego ciągu w skrypcie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="ec9e5-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="ec9e5-188">W tym przykładzie skrypt ma hello danych wejściowych z grupy zabezpieczeń sieci (NSG) i stosuje je toohello maszyny wirtualne w planie odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="ec9e5-189">Toodetect hello skryptu, jakiego planu odzyskiwania jest uruchomiona można użyć w kontekście planu odzyskiwania hello:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="ec9e5-190">tooapply istniejącej grupy NSG, musisz znać nazwę grupy NSG hello oraz nazwę grupy zasobów NSG hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="ec9e5-191">Użyj tych zmiennych jako dane wejściowe dla skryptów planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="ec9e5-192">toodo, Utwórz dwie zmienne w hello zasoby konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="ec9e5-193">Dodaj nazwę hello hello planu odzyskiwania, który tworzysz hello parametrów jako prefiksu nazwy zmiennej toohello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="ec9e5-194">Utwórz nazwę zmiennej toostore hello NSG.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="ec9e5-195">Dodaj prefiks nazwy zmiennej toohello przy użyciu nazwy hello hello planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Utwórz zmienną Nazwa grupy NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="ec9e5-197">Utwórz nazwę grupy zasobów NSG hello toostore zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="ec9e5-198">Dodaj prefiks nazwy zmiennej toohello przy użyciu nazwy hello hello planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Tworzenie grupy NSG Nazwa grupy zasobów](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="ec9e5-200">W skrypcie hello Użyj hello następujące wartości zmiennych hello tooget kodu odwołania:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="ec9e5-201">Użyj hello zmiennych w hello runbook tooapply hello NSG toohello interfejs sieciowy hello przełączona w tryb failover maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="ec9e5-202">Dla każdego planu odzyskiwania należy utworzyć zmienne niezależne, dzięki czemu można ponownie użyć skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="ec9e5-203">Dodaj prefiks przy użyciu nazwy planu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="ec9e5-204">Pełne, end-to-end skryptu dla tego scenariusza, zobacz [dodać publicznych adresów IP i NSG tooVMs podczas testowania trybu failover planu odzyskiwania usługi Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="ec9e5-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="ec9e5-205">Użyj toostore zmiennej złożone więcej informacji</span><span class="sxs-lookup"><span data-stu-id="ec9e5-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="ec9e5-206">Rozważmy scenariusz, w którym ma zostać tooturn jednego skryptu, na publiczny adres IP na określonych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="ec9e5-207">W innym scenariuszu może być tooapply różne grupy NSG na różnych maszynach wirtualnych (a nie na wszystkich maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="ec9e5-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="ec9e5-208">Możesz wprowadzić skrypt, który jest wielokrotnego użytku dla każdego planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="ec9e5-209">Każdy plan odzyskiwania może mieć zmiennej liczbę maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="ec9e5-210">Na przykład odzyskiwania SharePoint, ma dwa końce frontonu.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="ec9e5-211">Aplikacja podstawowe — biznesowych (LOB) ma tylko jeden frontonu.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="ec9e5-212">Nie można utworzyć oddzielne zmienne dla każdego planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="ec9e5-213">W hello poniższy przykład, firma Microsoft używa nowe techniki i utworzyć [zmiennej złożone](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) w zasobów konta usługi Automatyzacja Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="ec9e5-214">W tym celu określania wielu wartości.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="ec9e5-215">Należy użyć programu Azure PowerShell toocomplete hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="ec9e5-216">W programie PowerShell Zaloguj tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="ec9e5-217">Parametry hello toostore, Utwórz zmienną złożone hello przy użyciu nazwy hello hello planu odzyskiwania:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="ec9e5-218">W tej zmiennej złożone **VMDetails** hello chronione maszyny Wirtualnej jest hello identyfikator maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="ec9e5-219">tooget hello identyfikator maszyny Wirtualnej w hello portalu Azure, Wyświetl hello właściwości maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="ec9e5-220">Witaj Poniższy zrzut ekranu przedstawia zmiennej, która przechowuje informacje szczegółowe hello dwóch maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Użyj hello identyfikator maszyny Wirtualnej jako hello identyfikator GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="ec9e5-222">Użyj tej zmiennej w elemencie runbook.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-222">Use this variable in your runbook.</span></span> <span data-ttu-id="ec9e5-223">Jeśli hello wskazał identyfikator GUID maszyny Wirtualnej znajduje się w kontekście planu odzyskiwania hello, zastosuj hello NSG na powitania maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="ec9e5-224">W elemencie runbook pętli maszyn wirtualnych hello kontekstu planu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="ec9e5-225">Sprawdź, czy hello maszyna wirtualna istnieje w **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="ec9e5-226">Jeśli istnieje, uzyskać dostęp do właściwości hello hello zmiennej tooapply hello NSG:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="ec9e5-227">Hello sam skryptu służącego do planów odzyskiwania inny.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="ec9e5-228">Wprowadź różne parametry przechowując hello wartość, która odpowiada tooa planu odzyskiwania w różnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="ec9e5-229">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="ec9e5-229">Sample scripts</span></span>

<span data-ttu-id="ec9e5-230">toodeploy przykładowe skrypty tooyour konta automatyzacji, kliknij przycisk hello **wdrażanie tooAzure** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="ec9e5-231">[![Wdrażanie tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="ec9e5-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="ec9e5-232">Innym przykładem Zobacz powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="ec9e5-232">For another example, see hello following video.</span></span> <span data-ttu-id="ec9e5-233">Jednak przedstawia sposób toorecover tooAzure aplikacji WordPress dwuwarstwowa:</span><span class="sxs-lookup"><span data-stu-id="ec9e5-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="ec9e5-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ec9e5-234">Additional resources</span></span>
* [<span data-ttu-id="ec9e5-235">Azure automatyzacji usługi konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="ec9e5-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="ec9e5-236">Omówienie usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="ec9e5-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Omówienie usługi Automatyzacja Azure")
* [<span data-ttu-id="ec9e5-237">Azure Automation przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="ec9e5-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "usługi Automatyzacja Azure przykładowe skrypty")
