---
title: aaaMigrate konto automatyzacji i zasoby | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toomove automatyzacji konto usługi Automatyzacja Azure i powiązanych zasobów z tooanother jedną subskrypcję."
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
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="8265c-103">Migrowanie kont automatyzacji i zasobów</span><span class="sxs-lookup"><span data-stu-id="8265c-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="8265c-104">Dla konta automatyzacji i jej zasobach skojarzone (tj. zasoby, elementy runbook, modułów, itp.), które zostały utworzone w portalu Azure hello i chcesz toomigrate od jednego zasobu grupy tooanother lub z jedną subskrypcją tooanother, można wykonać to prosty sposób z Witaj [przenoszenia zasobów](../azure-resource-manager/resource-group-move-resources.md) funkcja dostępna w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8265c-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="8265c-105">Jednak przed wykonaniem tej akcji, należy najpierw przejrzeć następujące hello [listę kontrolną przed przeniesieniem zasobów](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) i ponadto hello poniższej tooAutomation określonej listy.</span><span class="sxs-lookup"><span data-stu-id="8265c-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="8265c-106">Witaj docelowej subskrypcji/grupy zasobów musi być w tym samym regionie co hello źródła.</span><span class="sxs-lookup"><span data-stu-id="8265c-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="8265c-107">To znaczy, konta automatyzacji nie można przenieść w regionach.</span><span class="sxs-lookup"><span data-stu-id="8265c-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="8265c-108">Podczas przenoszenia zasobów (np. elementy runbook, zadania, itp.), zarówno hello źródłowej grupy, jak i grupy docelowej hello są zablokowane na czas trwania operacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="8265c-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="8265c-109">Zapisu i usuwania działań są zablokowane na powitania grup dopiero po zakończeniu przenoszenia hello.</span><span class="sxs-lookup"><span data-stu-id="8265c-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="8265c-110">Wszystkie elementy runbook lub zmienne, które odwołują się do Identyfikatora zasobu lub subskrypcji z istniejącej subskrypcji hello należy toobe zaktualizowane po zakończeniu migracji.</span><span class="sxs-lookup"><span data-stu-id="8265c-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="8265c-111">Ta funkcja nie obsługuje przenoszenia zasobów automatyzacji klasycznego.</span><span class="sxs-lookup"><span data-stu-id="8265c-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="8265c-112">Konto automatyzacji za pomocą portalu hello hello toomove</span><span class="sxs-lookup"><span data-stu-id="8265c-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="8265c-113">Twoje konto usługi Automatyzacja kliknij **Przenieś** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="8265c-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="8265c-114">![Przenieś opcji](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="8265c-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="8265c-115">Na powitania **przenoszenia zasobów** bloku, należy pamiętać, że Twoje konto usługi Automatyzacja i z grup zasobów stanowi tooboth powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="8265c-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="8265c-116">Wybierz hello **subskrypcji** i **grupy zasobów** z list rozwijanych hello lub opcji wybierz hello **Utwórz nową grupę zasobów** , a następnie wprowadź nazwę nowej grupy zasobów w Witaj pola.</span><span class="sxs-lookup"><span data-stu-id="8265c-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="8265c-117">Przejrzyj i wybierz hello wyboru tooacknowledge możesz *zrozumieć narzędzia i skrypty będą potrzeby toobe zaktualizowane toouse nowych identyfikatorów zasobów. po przeniesieniu zasobów* , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8265c-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="8265c-118">![Przenieś bloku zasobów](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="8265c-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="8265c-119">Ta akcja potrwa kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8265c-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="8265c-120">W **powiadomienia**, zostaną wyświetlone ze stanem każda akcja ma miejsce — Weryfikacja, migracji, a następnie finally, gdy zostanie ukończona.</span><span class="sxs-lookup"><span data-stu-id="8265c-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="8265c-121">toomove hello konta automatyzacji za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8265c-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="8265c-122">toomove istniejącej grupy zasobów tooanother zasobów automatyzacji lub subskrypcji, użyj hello **Get-AzureRmResource** polecenia cmdlet tooget hello określonego konta automatyzacji, a następnie **AzureRmResource przenoszenia** Przenieś hello tooperform polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8265c-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="8265c-123">Hello pierwszym przykładzie pokazano, jak obiekt automatyzacji toomove konta tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="8265c-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="8265c-124">Po wykonaniu hello powyżej przykładowy kod będzie zostanie wyświetlony monit o tooverify ma tooperform tej akcji.</span><span class="sxs-lookup"><span data-stu-id="8265c-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="8265c-125">Po kliknięciu **tak** i umożliwić hello tooproceed skryptu, nie będziesz otrzymywać powiadomienia, podczas wykonywania migracji hello.</span><span class="sxs-lookup"><span data-stu-id="8265c-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="8265c-126">Nowa subskrypcja tooa toomove zawierać wartość hello *DestinationSubscriptionId* parametru.</span><span class="sxs-lookup"><span data-stu-id="8265c-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="8265c-127">Podobnie jak w poprzednim przykładzie hello, będzie zostanie wyświetlony monit o tooconfirm hello przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="8265c-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="8265c-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8265c-128">Next steps</span></span>
* <span data-ttu-id="8265c-129">Aby uzyskać więcej informacji na temat przenoszenia grupy zasobów toonew zasobów lub subskrypcji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="8265c-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="8265c-130">Aby uzyskać więcej informacji na temat opartej na rolach kontroli dostępu w usłudze Automatyzacja Azure można znaleźć zbyt[kontroli dostępu opartej na rolach w automatyzacji Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="8265c-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="8265c-131">Zobacz toolearn o poleceniach cmdlet programu PowerShell do zarządzania subskrypcją, [przy użyciu programu Azure PowerShell z usługą Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="8265c-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="8265c-132">Zobacz toolearn funkcje portalu do zarządzania subskrypcją, [przy użyciu zasobów toomanage Azure Portal hello](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8265c-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
