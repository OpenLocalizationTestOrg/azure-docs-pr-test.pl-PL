---
title: "PowerShell przykład — monitor — skali-elastycznej puli Azure SQL bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell do monitorowania i skalowania puli elastycznej SQL w bazie danych SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="b342c-103">Monitorowanie i skalowania puli elastycznej SQL w bazie danych SQL Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b342c-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="b342c-104">Ten przykładowy skrypt programu PowerShell monitoruje metryk wydajności puli elastycznej, skaluje go na wyższy poziom wydajności i tworzy regułę alertu w jednym z metryk wydajności.</span><span class="sxs-lookup"><span data-stu-id="b342c-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b342c-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b342c-105">Sample script</span></span>

<span data-ttu-id="b342c-106">[!code-powershell[główne](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "monitora i skali Pojedyncza baza danych SQL")]</span><span class="sxs-lookup"><span data-stu-id="b342c-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b342c-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b342c-107">Clean up deployment</span></span>

<span data-ttu-id="b342c-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="b342c-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b342c-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b342c-109">Script explanation</span></span>

<span data-ttu-id="b342c-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="b342c-110">This script uses the following commands.</span></span> <span data-ttu-id="b342c-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b342c-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b342c-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b342c-112">Command</span></span> | <span data-ttu-id="b342c-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b342c-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="b342c-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b342c-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b342c-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b342c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b342c-116">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b342c-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b342c-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="b342c-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b342c-118">Nowe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b342c-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b342c-119">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="b342c-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b342c-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b342c-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b342c-121">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b342c-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b342c-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="b342c-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="b342c-123">Przedstawia informacje o użyciu rozmiar bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b342c-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="b342c-124">Dodaj AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="b342c-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="b342c-125">Dodaje lub aktualizuje regułę alertu metryki.</span><span class="sxs-lookup"><span data-stu-id="b342c-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="b342c-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b342c-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="b342c-127">Aktualizuje właściwości puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="b342c-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="b342c-128">Dodaj AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="b342c-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="b342c-129">Ustawia reguły alertu automatycznie monitorować jednostek Dtu w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="b342c-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="b342c-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b342c-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b342c-131">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b342c-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b342c-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b342c-132">Next steps</span></span>

<span data-ttu-id="b342c-133">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b342c-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b342c-134">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b342c-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
