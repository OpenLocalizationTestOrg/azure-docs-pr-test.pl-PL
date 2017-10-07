---
title: "Baza danych Azure SQL przykład monitora skali — pojedynczy aaaPowerShell | Dokumentacja firmy Microsoft"
description: "Azure PowerShell przykładowy skrypt toomonitor i skalowania pojedynczej bazy danych Azure SQL"
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="5f6a6-103">Użyj programu PowerShell toomonitor i skalowania pojedynczej bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="5f6a6-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="5f6a6-104">Ten przykładowy skrypt programu PowerShell się, że monitory hello metryki wydajności bazy danych, skaluje go tooa wyższy poziom wydajności i tworzy regułę alertu w jednym z hello metryki wydajności.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5f6a6-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5f6a6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5f6a6-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5f6a6-106">Clean up deployment</span></span>

<span data-ttu-id="5f6a6-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5f6a6-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5f6a6-108">Script explanation</span></span>

<span data-ttu-id="5f6a6-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-109">This script uses hello following commands.</span></span> <span data-ttu-id="5f6a6-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5f6a6-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5f6a6-111">Command</span></span> | <span data-ttu-id="5f6a6-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5f6a6-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="5f6a6-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f6a6-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5f6a6-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5f6a6-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="5f6a6-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5f6a6-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5f6a6-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="5f6a6-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="5f6a6-118">Zawiera informacje o użyciu rozmiar hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="5f6a6-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5f6a6-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="5f6a6-120">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="5f6a6-121">Dodaj AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="5f6a6-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="5f6a6-122">Ustawia reguły alertu tooautomatically monitora jednostek Dtu w hello przyszłych.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="5f6a6-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f6a6-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5f6a6-124">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5f6a6-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5f6a6-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f6a6-125">Next steps</span></span>

<span data-ttu-id="5f6a6-126">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f6a6-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5f6a6-127">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5f6a6-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
