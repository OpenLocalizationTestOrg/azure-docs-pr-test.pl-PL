---
title: "Migrowanie kont automatyzacji i zasobów | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak przenieść konto usługi Automatyzacja w automatyzacji Azure oraz zasoby skojarzone z jedną subskrypcją."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="0f787-103">Migrowanie kont automatyzacji i zasobów</span><span class="sxs-lookup"><span data-stu-id="0f787-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="0f787-104">Dla kont automatyzacji i jej zasobach skojarzone (tj. zasoby, elementy runbook, modułów, itp.), które zostały utworzone w portalu Azure i chcesz przeprowadzić migrację między grupami zasobów lub między jedną subskrypcję do innej, można wykonać to prosty sposób z [przenoszenia zasobów](../azure-resource-manager/resource-group-move-resources.md) funkcji dostępnej w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f787-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="0f787-105">Jednak przed wykonaniem tej akcji, należy najpierw przejrzeć następujące [listę kontrolną przed przeniesieniem zasobów](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) , a ponadto na poniższej liście specyficzne dla automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="0f787-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="0f787-106">Docelowej subskrypcji/grupy zasobów musi być w tym samym regionie co źródło.</span><span class="sxs-lookup"><span data-stu-id="0f787-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="0f787-107">To znaczy, konta automatyzacji nie można przenieść w regionach.</span><span class="sxs-lookup"><span data-stu-id="0f787-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="0f787-108">Podczas przenoszenia zasobów (np. elementy runbook, zadania, itp.), zarówno grupy źródłowej i docelowej grupy są zablokowane na czas trwania operacji.</span><span class="sxs-lookup"><span data-stu-id="0f787-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="0f787-109">Zapisu i usuwania działań są blokowane w grupach, dopiero po zakończeniu przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="0f787-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="0f787-110">Wszystkie elementy runbook lub zmienne, które odwołują się do Identyfikatora zasobu lub subskrypcji z istniejącej subskrypcji zostanie muszą zostać zaktualizowane po zakończeniu migracji.</span><span class="sxs-lookup"><span data-stu-id="0f787-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="0f787-111">Ta funkcja nie obsługuje przenoszenia zasobów automatyzacji klasycznego.</span><span class="sxs-lookup"><span data-stu-id="0f787-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="0f787-112">Aby przenieść przy użyciu portalu konta automatyzacji</span><span class="sxs-lookup"><span data-stu-id="0f787-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="0f787-113">Twoje konto usługi Automatyzacja kliknij **Przenieś** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="0f787-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="0f787-114">![Przenieś opcji](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="0f787-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="0f787-115">Na **przenoszenia zasobów** bloku, należy pamiętać, że stanowi zasobów związanych z zarówno konto automatyzacji, jak i z grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="0f787-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="0f787-116">Wybierz **subskrypcji** i **grupy zasobów** z listy rozwijanej lub wybierz opcję **Utwórz nową grupę zasobów** , a następnie wprowadź nazwę nowej grupy zasobów w polu.</span><span class="sxs-lookup"><span data-stu-id="0f787-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="0f787-117">Przejrzyj i zaznacz pole wyboru, musisz potwierdzić *zrozumieć narzędzia i skrypty musi zostać zaktualizowany w celu użycia nowych identyfikatorów zasobów. po przeniesieniu zasobów* , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f787-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="0f787-118">![Przenieś bloku zasobów](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="0f787-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="0f787-119">Ta akcja potrwa kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0f787-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="0f787-120">W **powiadomienia**, zostaną wyświetlone ze stanem każda akcja ma miejsce — Weryfikacja, migracji, a następnie finally, gdy zostanie ukończona.</span><span class="sxs-lookup"><span data-stu-id="0f787-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="0f787-121">Aby przenieść konto automatyzacji za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f787-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="0f787-122">Aby przenieść istniejące zasoby automatyzacji do innej grupy zasobów lub subskrypcji, należy użyć **Get-AzureRmResource** polecenia cmdlet można pobrać określonego konta automatyzacji, a następnie **AzureRmResource przenoszenia** polecenia cmdlet do wykonania czynności.</span><span class="sxs-lookup"><span data-stu-id="0f787-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="0f787-123">Pierwszym przykładzie pokazano, jak można przenieść konto automatyzacji do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0f787-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="0f787-124">Po wykonaniu powyższych przykładów kodu, pojawi się monit, aby sprawdzić, czy chcesz wykonać tę akcję.</span><span class="sxs-lookup"><span data-stu-id="0f787-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="0f787-125">Po kliknięciu **tak** i umożliwiają skryptu kontynuować, nie będziesz otrzymywać powiadomienia, podczas wykonywania migracji.</span><span class="sxs-lookup"><span data-stu-id="0f787-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="0f787-126">Aby przejść do nowej subskrypcji, zawierają wartość *DestinationSubscriptionId* parametru.</span><span class="sxs-lookup"><span data-stu-id="0f787-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="0f787-127">Podobnie jak w poprzednim przykładzie, zostanie wyświetlony monit o potwierdzenie przeniesienie.</span><span class="sxs-lookup"><span data-stu-id="0f787-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0f787-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f787-128">Next steps</span></span>
* <span data-ttu-id="0f787-129">Aby uzyskać więcej informacji na temat przenoszenia zasobów do nowej grupy zasobów lub subskrypcji, zobacz [przenoszenia zasobów do nowej grupy zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="0f787-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="0f787-130">Więcej informacji na temat kontroli dostępu opartej na rolach w usłudze Automatyzacja platformy Azure można znaleźć w temacie [Kontrola dostępu oparta na rolach w usłudze Automatyzacja platformy Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0f787-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="0f787-131">Aby dowiedzieć się więcej na temat poleceń cmdlet programu PowerShell do zarządzania subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="0f787-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="0f787-132">Aby dowiedzieć się więcej o funkcjach portalu do zarządzania subskrypcją, zobacz [przy użyciu portalu Azure do zarządzania zasobami](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f787-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
