---
title: "aaaScheduler Dokumentacja poleceń cmdlet programu PowerShell"
description: "Dokumentacja poleceń cmdlet programu PowerShell harmonogramu"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="feaad-103">Dokumentacja poleceń cmdlet programu PowerShell harmonogramu</span><span class="sxs-lookup"><span data-stu-id="feaad-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="feaad-104">Witaj w poniższej tabeli opisano i łączy strona referencyjna toohello każdego hello głównych poleceń cmdlet Harmonogram systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="feaad-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="feaad-105">tooinstall programu Azure PowerShell i skojarzyć go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="feaad-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="feaad-106">Aby uzyskać więcej informacji na temat [poleceń cmdlet usługi Azure Resource Manager](/powershell/azure/overview), zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="feaad-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="feaad-107">Polecenie cmdlet</span><span class="sxs-lookup"><span data-stu-id="feaad-107">Cmdlet</span></span> | <span data-ttu-id="feaad-108">Opis polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="feaad-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="feaad-109">Wyłącz AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="feaad-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="feaad-110">Wyłącza kolekcji zadań.</span><span class="sxs-lookup"><span data-stu-id="feaad-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="feaad-111">Włącz AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="feaad-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="feaad-112">Umożliwia kolekcji zadań.</span><span class="sxs-lookup"><span data-stu-id="feaad-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="feaad-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="feaad-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="feaad-114">Pobiera harmonogram zadań.</span><span class="sxs-lookup"><span data-stu-id="feaad-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="feaad-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="feaad-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="feaad-116">Pobiera zadań kolekcji.</span><span class="sxs-lookup"><span data-stu-id="feaad-116">Gets job collections.</span></span> |
| [<span data-ttu-id="feaad-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="feaad-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="feaad-118">Pobiera Historia zadania.</span><span class="sxs-lookup"><span data-stu-id="feaad-118">Gets job history.</span></span> |
| [<span data-ttu-id="feaad-119">Nowe AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="feaad-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="feaad-120">Tworzy zadanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="feaad-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="feaad-121">Nowe AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="feaad-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="feaad-122">Tworzy kolekcję zadań.</span><span class="sxs-lookup"><span data-stu-id="feaad-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="feaad-123">Nowe AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="feaad-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="feaad-124">Tworzy zadanie kolejki magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="feaad-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="feaad-125">Nowe AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="feaad-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="feaad-126">Tworzy zadanie tematów magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="feaad-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="feaad-127">Nowe AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="feaad-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="feaad-128">Tworzy zadanie kolejki magazynu.</span><span class="sxs-lookup"><span data-stu-id="feaad-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="feaad-129">Usuń AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="feaad-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="feaad-130">Usuwa zadania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="feaad-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="feaad-131">Usuń AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="feaad-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="feaad-132">Usuwa kolekcji zadań.</span><span class="sxs-lookup"><span data-stu-id="feaad-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="feaad-133">Zestaw AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="feaad-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="feaad-134">Modyfikuje zadania harmonogramu HTTP.</span><span class="sxs-lookup"><span data-stu-id="feaad-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="feaad-135">Zestaw AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="feaad-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="feaad-136">Modyfikuje kolekcji zadań.</span><span class="sxs-lookup"><span data-stu-id="feaad-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="feaad-137">Zestaw AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="feaad-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="feaad-138">Modyfikuje zadania kolejki magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="feaad-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="feaad-139">Zestaw AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="feaad-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="feaad-140">Modyfikuje zadania tematów magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="feaad-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="feaad-141">Zestaw AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="feaad-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="feaad-142">Modyfikuje zadanie kolejki magazynu.</span><span class="sxs-lookup"><span data-stu-id="feaad-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="feaad-143">Aby uzyskać szczegółowe informacje można uruchomić dowolną z następujących poleceń cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="feaad-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="feaad-144">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="feaad-144">See Also</span></span>
 [<span data-ttu-id="feaad-145">Co to jest Scheduler?</span><span class="sxs-lookup"><span data-stu-id="feaad-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="feaad-146">Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="feaad-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="feaad-147">Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="feaad-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="feaad-148">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="feaad-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="feaad-149">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="feaad-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="feaad-150">Wysoka dostępność i niezawodność usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="feaad-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="feaad-151">Limity, wartości domyślne i kody błędów usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="feaad-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="feaad-152">Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="feaad-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

