---
title: "aaaPowerShell przykład restore-kopii zapasowej — usługi Azure SQL database | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toorestore bazy danych Azure SQL z kopii zapasowych geograficznie nadmiarowego Azure PowerShell"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="94fc6-103">Użyj programu PowerShell toorestore bazy danych Azure SQL z kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="94fc6-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="94fc6-104">Ten przykładowy skrypt programu PowerShell przywraca bazę danych Azure SQL z geograficznie nadmiarowej kopii zapasowej, przywrócenie usuniętych Azure SQL bazy danych tooits najnowszej kopii zapasowej i przywraca tooa bazy danych Azure SQL dla punktu określonych w czasie.</span><span class="sxs-lookup"><span data-stu-id="94fc6-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="94fc6-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="94fc6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="94fc6-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="94fc6-106">Clean up deployment</span></span>

<span data-ttu-id="94fc6-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="94fc6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="94fc6-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="94fc6-108">Script explanation</span></span>

<span data-ttu-id="94fc6-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="94fc6-109">This script uses hello following commands.</span></span> <span data-ttu-id="94fc6-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="94fc6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="94fc6-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="94fc6-111">Command</span></span> | <span data-ttu-id="94fc6-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94fc6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="94fc6-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="94fc6-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="94fc6-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="94fc6-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="94fc6-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="94fc6-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="94fc6-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="94fc6-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="94fc6-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="94fc6-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="94fc6-118">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="94fc6-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="94fc6-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="94fc6-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="94fc6-120">Pobiera geograficznie nadmiarowego kopii zapasowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="94fc6-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="94fc6-121">Przywracanie AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="94fc6-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="94fc6-122">Przywraca bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="94fc6-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="94fc6-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="94fc6-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="94fc6-124">Usuwa z bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="94fc6-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="94fc6-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="94fc6-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="94fc6-126">Pobiera usuniętej bazy danych, które można przywrócić.</span><span class="sxs-lookup"><span data-stu-id="94fc6-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="94fc6-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="94fc6-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="94fc6-128">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="94fc6-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94fc6-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94fc6-129">Next steps</span></span>

<span data-ttu-id="94fc6-130">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="94fc6-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="94fc6-131">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="94fc6-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
