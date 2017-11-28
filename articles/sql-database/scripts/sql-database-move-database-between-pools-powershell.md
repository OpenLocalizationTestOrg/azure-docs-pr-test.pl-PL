---
title: "puli elastycznej bazy danych SQL Azure SQL przenoszenia przykład aaaPowerShell | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toomove między pule elastyczne przy użyciu programu PowerShell bazy danych SQL Azure PowerShell"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="f291f-103">Użyj programu PowerShell toocreate elastycznych pul i przenoszenie baz danych między pul elastycznych</span><span class="sxs-lookup"><span data-stu-id="f291f-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="f291f-104">Ten przykładowy skrypt programu PowerShell tworzy dwie pule elastyczne i przenosi bazy danych z jednej puli elastycznej do innej puli elastycznej i przenosi bazy danych poza poziom wydajności puli elastycznej tooa pojedynczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f291f-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f291f-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f291f-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f291f-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f291f-106">Clean up deployment</span></span>

<span data-ttu-id="f291f-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="f291f-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f291f-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f291f-108">Script explanation</span></span>

<span data-ttu-id="f291f-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="f291f-109">This script uses hello following commands.</span></span> <span data-ttu-id="f291f-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f291f-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f291f-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f291f-111">Command</span></span> | <span data-ttu-id="f291f-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f291f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f291f-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f291f-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f291f-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f291f-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f291f-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="f291f-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f291f-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="f291f-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f291f-117">Nowe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="f291f-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="f291f-118">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="f291f-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="f291f-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f291f-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f291f-120">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f291f-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f291f-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f291f-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="f291f-122">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="f291f-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f291f-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f291f-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f291f-124">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f291f-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f291f-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f291f-125">Next steps</span></span>

<span data-ttu-id="f291f-126">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f291f-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f291f-127">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f291f-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
