---
title: "Baza danych SQL Azure PowerShell aktywny przykład geograficznie replikacji — pojedynczy | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell do konfigurowania aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL"
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
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="b0c12-103">Aby skonfigurować aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0c12-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="b0c12-104">Ten przykładowy skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL i awaryjnie do repliki pomocniczej bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="b0c12-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="b0c12-105">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="b0c12-105">Sample scripts</span></span>

<span data-ttu-id="b0c12-106">[!code-powershell[główne](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Konfigurowanie aktywna replikacja geograficzna dla pojedynczej bazy danych")]</span><span class="sxs-lookup"><span data-stu-id="b0c12-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b0c12-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b0c12-107">Clean up deployment</span></span>

<span data-ttu-id="b0c12-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="b0c12-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b0c12-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b0c12-109">Script explanation</span></span>

<span data-ttu-id="b0c12-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="b0c12-110">This script uses the following commands.</span></span> <span data-ttu-id="b0c12-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b0c12-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b0c12-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b0c12-112">Command</span></span> | <span data-ttu-id="b0c12-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b0c12-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b0c12-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b0c12-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b0c12-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b0c12-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b0c12-116">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b0c12-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b0c12-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="b0c12-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b0c12-118">Nowe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b0c12-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b0c12-119">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="b0c12-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b0c12-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b0c12-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="b0c12-121">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="b0c12-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="b0c12-122">Nowe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b0c12-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="b0c12-123">Tworzy pomocniczej bazy danych dla istniejącej bazy danych i rozpoczyna się replikacja danych.</span><span class="sxs-lookup"><span data-stu-id="b0c12-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="b0c12-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b0c12-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="b0c12-125">Pobiera jeden lub więcej baz danych.</span><span class="sxs-lookup"><span data-stu-id="b0c12-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="b0c12-126">Zestaw AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b0c12-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="b0c12-127">Zmienia pomocniczej bazy danych jako głównej zainicjować trybu failover.</span><span class="sxs-lookup"><span data-stu-id="b0c12-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="b0c12-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="b0c12-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="b0c12-129">Pobiera linki — replikacja geograficzna między bazą danych SQL Azure i grupy zasobów lub SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0c12-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="b0c12-130">Usuń AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b0c12-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="b0c12-131">Kończy replikacji danych między bazą danych SQL i dodatkowej określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b0c12-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="b0c12-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b0c12-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b0c12-133">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b0c12-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b0c12-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0c12-134">Next steps</span></span>

<span data-ttu-id="b0c12-135">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0c12-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b0c12-136">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b0c12-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
