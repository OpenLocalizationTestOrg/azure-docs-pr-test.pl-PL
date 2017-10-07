---
title: "aaaPowerShell przykład aktywny geograficznie replikacji — pojedynczy Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Azure PowerShell przykładowy skrypt tooset się aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL"
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
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="4d120-103">Użyj programu PowerShell tooconfigure aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="4d120-103">Use PowerShell tooconfigure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="4d120-104">Ten przykładowy skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL i awaryjnie tooa repliki pomocniczej bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="4d120-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="4d120-105">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="4d120-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4d120-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4d120-106">Clean up deployment</span></span>

<span data-ttu-id="4d120-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="4d120-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="4d120-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="4d120-108">Script explanation</span></span>

<span data-ttu-id="4d120-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="4d120-109">This script uses hello following commands.</span></span> <span data-ttu-id="4d120-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="4d120-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4d120-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="4d120-111">Command</span></span> | <span data-ttu-id="4d120-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4d120-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4d120-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4d120-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4d120-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="4d120-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4d120-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="4d120-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="4d120-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="4d120-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="4d120-117">Nowe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="4d120-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="4d120-118">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="4d120-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="4d120-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="4d120-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="4d120-120">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="4d120-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="4d120-121">Nowe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="4d120-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="4d120-122">Tworzy pomocniczej bazy danych dla istniejącej bazy danych i rozpoczyna się replikacja danych.</span><span class="sxs-lookup"><span data-stu-id="4d120-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="4d120-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="4d120-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="4d120-124">Pobiera jeden lub więcej baz danych.</span><span class="sxs-lookup"><span data-stu-id="4d120-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="4d120-125">Zestaw AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="4d120-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="4d120-126">Zmienia awarię podstawowej tooinitiate toobe dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4d120-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="4d120-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="4d120-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="4d120-128">Pobiera hello — replikacja geograficzna łącza między bazą danych SQL Azure i grupy zasobów lub SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d120-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="4d120-129">Usuń AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="4d120-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="4d120-130">Kończy replikacji danych między bazą danych SQL i hello określonego dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4d120-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="4d120-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4d120-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4d120-132">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="4d120-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4d120-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d120-133">Next steps</span></span>

<span data-ttu-id="4d120-134">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4d120-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4d120-135">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4d120-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
