---
title: "Baza danych Azure SQL przykład monitora skali — pojedynczy programu PowerShell | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell do monitorowania i skalowania pojedynczej bazy danych Azure SQL"
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
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="e830f-103">Aby monitorować i skalowania pojedynczej bazy danych SQL za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e830f-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="e830f-104">Ten przykładowy skrypt programu PowerShell monitoruje metryki wydajności bazy danych, skaluje go na wyższy poziom wydajności i tworzy regułę alertu w jednym z metryk wydajności.</span><span class="sxs-lookup"><span data-stu-id="e830f-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="e830f-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="e830f-105">Sample script</span></span>

<span data-ttu-id="e830f-106">[!code-powershell[główne](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "monitora i skali Pojedyncza baza danych SQL")]</span><span class="sxs-lookup"><span data-stu-id="e830f-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e830f-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e830f-107">Clean up deployment</span></span>

<span data-ttu-id="e830f-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="e830f-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="e830f-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="e830f-109">Script explanation</span></span>

<span data-ttu-id="e830f-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="e830f-110">This script uses the following commands.</span></span> <span data-ttu-id="e830f-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e830f-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e830f-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="e830f-112">Command</span></span> | <span data-ttu-id="e830f-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e830f-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="e830f-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e830f-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e830f-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="e830f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e830f-116">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="e830f-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="e830f-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="e830f-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="e830f-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="e830f-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="e830f-119">Przedstawia informacje o użyciu rozmiar bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e830f-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="e830f-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e830f-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="e830f-121">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="e830f-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="e830f-122">Dodaj AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="e830f-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="e830f-123">Ustawia reguły alertu automatycznie monitorować jednostek Dtu w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="e830f-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="e830f-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e830f-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e830f-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e830f-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="e830f-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e830f-126">Next steps</span></span>

<span data-ttu-id="e830f-127">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e830f-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e830f-128">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e830f-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
