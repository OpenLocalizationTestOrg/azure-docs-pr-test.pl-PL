---
title: "przykład kopii Azure aaaPowerShell SQL server Nowa baza danych | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toocopy nowy serwer tooa bazy danych SQL Azure PowerShell"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="615bd-103">Użyj programu PowerShell toocopy nowy serwer tooa bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="615bd-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="615bd-104">Ten przykładowy skrypt programu PowerShell tworzy kopię istniejącej bazy danych w nowym serwerze.</span><span class="sxs-lookup"><span data-stu-id="615bd-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="615bd-105">Skopiuj nowy serwer tooa bazy danych</span><span class="sxs-lookup"><span data-stu-id="615bd-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="615bd-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="615bd-106">Clean up deployment</span></span>

<span data-ttu-id="615bd-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="615bd-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="615bd-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="615bd-108">Script explanation</span></span>

<span data-ttu-id="615bd-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="615bd-109">This script uses hello following commands.</span></span> <span data-ttu-id="615bd-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="615bd-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="615bd-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="615bd-111">Command</span></span> | <span data-ttu-id="615bd-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="615bd-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="615bd-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="615bd-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="615bd-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="615bd-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="615bd-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="615bd-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="615bd-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="615bd-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="615bd-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="615bd-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="615bd-118">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="615bd-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="615bd-119">Nowe AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="615bd-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="615bd-120">Tworzy kopię bazy danych, która używa hello migawki na powitania bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="615bd-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="615bd-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="615bd-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="615bd-122">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="615bd-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="615bd-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="615bd-123">Next steps</span></span>

<span data-ttu-id="615bd-124">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="615bd-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="615bd-125">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="615bd-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
