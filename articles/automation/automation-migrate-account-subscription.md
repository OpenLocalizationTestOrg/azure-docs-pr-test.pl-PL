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
# <a name="migrate-automation-account-and-resources"></a>Migrowanie kont automatyzacji i zasobów
Dla kont automatyzacji i jej zasobach skojarzone (tj. zasoby, elementy runbook, modułów, itp.), które zostały utworzone w portalu Azure i chcesz przeprowadzić migrację między grupami zasobów lub między jedną subskrypcję do innej, można wykonać to prosty sposób z [przenoszenia zasobów](../azure-resource-manager/resource-group-move-resources.md) funkcji dostępnej w portalu Azure. Jednak przed wykonaniem tej akcji, należy najpierw przejrzeć następujące [listę kontrolną przed przeniesieniem zasobów](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) , a ponadto na poniższej liście specyficzne dla automatyzacji.   

1. Docelowej subskrypcji/grupy zasobów musi być w tym samym regionie co źródło.  To znaczy, konta automatyzacji nie można przenieść w regionach.
2. Podczas przenoszenia zasobów (np. elementy runbook, zadania, itp.), zarówno grupy źródłowej i docelowej grupy są zablokowane na czas trwania operacji. Zapisu i usuwania działań są blokowane w grupach, dopiero po zakończeniu przenoszenia.  
3. Wszystkie elementy runbook lub zmienne, które odwołują się do Identyfikatora zasobu lub subskrypcji z istniejącej subskrypcji zostanie muszą zostać zaktualizowane po zakończeniu migracji.   

> [!NOTE]
> Ta funkcja nie obsługuje przenoszenia zasobów automatyzacji klasycznego.
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a>Aby przenieść przy użyciu portalu konta automatyzacji
1. Twoje konto usługi Automatyzacja kliknij **Przenieś** w górnej części bloku.<br> ![Przenieś opcji](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Na **przenoszenia zasobów** bloku, należy pamiętać, że stanowi zasobów związanych z zarówno konto automatyzacji, jak i z grup zasobów.  Wybierz **subskrypcji** i **grupy zasobów** z listy rozwijanej lub wybierz opcję **Utwórz nową grupę zasobów** , a następnie wprowadź nazwę nowej grupy zasobów w polu.  
3. Przejrzyj i zaznacz pole wyboru, musisz potwierdzić *zrozumieć narzędzia i skrypty musi zostać zaktualizowany w celu użycia nowych identyfikatorów zasobów. po przeniesieniu zasobów* , a następnie kliknij przycisk **OK**.<br> ![Przenieś bloku zasobów](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Ta akcja potrwa kilka minut.  W **powiadomienia**, zostaną wyświetlone ze stanem każda akcja ma miejsce — Weryfikacja, migracji, a następnie finally, gdy zostanie ukończona.     

## <a name="to-move-the-automation-account-using-powershell"></a>Aby przenieść konto automatyzacji za pomocą programu PowerShell
Aby przenieść istniejące zasoby automatyzacji do innej grupy zasobów lub subskrypcji, należy użyć **Get-AzureRmResource** polecenia cmdlet można pobrać określonego konta automatyzacji, a następnie **AzureRmResource przenoszenia** polecenia cmdlet do wykonania czynności.

Pierwszym przykładzie pokazano, jak można przenieść konto automatyzacji do nowej grupy zasobów.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Po wykonaniu powyższych przykładów kodu, pojawi się monit, aby sprawdzić, czy chcesz wykonać tę akcję.  Po kliknięciu **tak** i umożliwiają skryptu kontynuować, nie będziesz otrzymywać powiadomienia, podczas wykonywania migracji.  

Aby przejść do nowej subskrypcji, zawierają wartość *DestinationSubscriptionId* parametru.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Podobnie jak w poprzednim przykładzie, zostanie wyświetlony monit o potwierdzenie przeniesienie.  

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat przenoszenia zasobów do nowej grupy zasobów lub subskrypcji, zobacz [przenoszenia zasobów do nowej grupy zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md)
* Więcej informacji na temat kontroli dostępu opartej na rolach w usłudze Automatyzacja platformy Azure można znaleźć w temacie [Kontrola dostępu oparta na rolach w usłudze Automatyzacja platformy Azure](automation-role-based-access-control.md).
* Aby dowiedzieć się więcej na temat poleceń cmdlet programu PowerShell do zarządzania subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)
* Aby dowiedzieć się więcej o funkcjach portalu do zarządzania subskrypcją, zobacz [przy użyciu portalu Azure do zarządzania zasobami](../azure-resource-manager/resource-group-portal.md).
