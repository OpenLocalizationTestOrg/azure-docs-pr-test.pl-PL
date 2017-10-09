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
# <a name="migrate-automation-account-and-resources"></a>Migrowanie kont automatyzacji i zasobów
Dla konta automatyzacji i jej zasobach skojarzone (tj. zasoby, elementy runbook, modułów, itp.), które zostały utworzone w portalu Azure hello i chcesz toomigrate od jednego zasobu grupy tooanother lub z jedną subskrypcją tooanother, można wykonać to prosty sposób z Witaj [przenoszenia zasobów](../azure-resource-manager/resource-group-move-resources.md) funkcja dostępna w hello portalu Azure. Jednak przed wykonaniem tej akcji, należy najpierw przejrzeć następujące hello [listę kontrolną przed przeniesieniem zasobów](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) i ponadto hello poniższej tooAutomation określonej listy.   

1. Witaj docelowej subskrypcji/grupy zasobów musi być w tym samym regionie co hello źródła.  To znaczy, konta automatyzacji nie można przenieść w regionach.
2. Podczas przenoszenia zasobów (np. elementy runbook, zadania, itp.), zarówno hello źródłowej grupy, jak i grupy docelowej hello są zablokowane na czas trwania operacji hello hello. Zapisu i usuwania działań są zablokowane na powitania grup dopiero po zakończeniu przenoszenia hello.  
3. Wszystkie elementy runbook lub zmienne, które odwołują się do Identyfikatora zasobu lub subskrypcji z istniejącej subskrypcji hello należy toobe zaktualizowane po zakończeniu migracji.   

> [!NOTE]
> Ta funkcja nie obsługuje przenoszenia zasobów automatyzacji klasycznego.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>Konto automatyzacji za pomocą portalu hello hello toomove
1. Twoje konto usługi Automatyzacja kliknij **Przenieś** u góry bloku hello hello.<br> ![Przenieś opcji](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Na powitania **przenoszenia zasobów** bloku, należy pamiętać, że Twoje konto usługi Automatyzacja i z grup zasobów stanowi tooboth powiązane zasoby.  Wybierz hello **subskrypcji** i **grupy zasobów** z list rozwijanych hello lub opcji wybierz hello **Utwórz nową grupę zasobów** , a następnie wprowadź nazwę nowej grupy zasobów w Witaj pola.  
3. Przejrzyj i wybierz hello wyboru tooacknowledge możesz *zrozumieć narzędzia i skrypty będą potrzeby toobe zaktualizowane toouse nowych identyfikatorów zasobów. po przeniesieniu zasobów* , a następnie kliknij przycisk **OK**.<br> ![Przenieś bloku zasobów](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Ta akcja potrwa kilka minut toocomplete.  W **powiadomienia**, zostaną wyświetlone ze stanem każda akcja ma miejsce — Weryfikacja, migracji, a następnie finally, gdy zostanie ukończona.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove hello konta automatyzacji za pomocą programu PowerShell
toomove istniejącej grupy zasobów tooanother zasobów automatyzacji lub subskrypcji, użyj hello **Get-AzureRmResource** polecenia cmdlet tooget hello określonego konta automatyzacji, a następnie **AzureRmResource przenoszenia** Przenieś hello tooperform polecenia cmdlet.

Hello pierwszym przykładzie pokazano, jak obiekt automatyzacji toomove konta tooa nową grupę zasobów.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Po wykonaniu hello powyżej przykładowy kod będzie zostanie wyświetlony monit o tooverify ma tooperform tej akcji.  Po kliknięciu **tak** i umożliwić hello tooproceed skryptu, nie będziesz otrzymywać powiadomienia, podczas wykonywania migracji hello.  

Nowa subskrypcja tooa toomove zawierać wartość hello *DestinationSubscriptionId* parametru.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Podobnie jak w poprzednim przykładzie hello, będzie zostanie wyświetlony monit o tooconfirm hello przenoszenia.  

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat przenoszenia grupy zasobów toonew zasobów lub subskrypcji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md)
* Aby uzyskać więcej informacji na temat opartej na rolach kontroli dostępu w usłudze Automatyzacja Azure można znaleźć zbyt[kontroli dostępu opartej na rolach w automatyzacji Azure](automation-role-based-access-control.md).
* Zobacz toolearn o poleceniach cmdlet programu PowerShell do zarządzania subskrypcją, [przy użyciu programu Azure PowerShell z usługą Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)
* Zobacz toolearn funkcje portalu do zarządzania subskrypcją, [przy użyciu zasobów toomanage Azure Portal hello](../azure-resource-manager/resource-group-portal.md).
