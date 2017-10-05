---
title: "PowerShell aktywny przykład puli replikację geograficzną usługa Azure SQL database | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell do konfigurowania aktywna replikacja geograficzna puli bazy danych Azure SQL"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: c1a495a8f9960ed60d8589dee9615e075f80c77b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="a5169-103">Aby skonfigurować aktywna replikacja geograficzna puli bazy danych Azure SQL za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5169-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="a5169-104">Ten przykładowy skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla bazy danych Azure SQL w puli elastycznej i awaryjnie do repliki pomocniczej bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="a5169-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="a5169-105">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="a5169-105">Sample scripts</span></span>

<span data-ttu-id="a5169-106">[!code-powershell[główne](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Konfigurowanie aktywna replikacja geograficzna dla puli elastycznej")]</span><span class="sxs-lookup"><span data-stu-id="a5169-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a5169-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a5169-107">Clean up deployment</span></span>

<span data-ttu-id="a5169-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="a5169-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a5169-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a5169-109">Script explanation</span></span>

<span data-ttu-id="a5169-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="a5169-110">This script uses the following commands.</span></span> <span data-ttu-id="a5169-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="a5169-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a5169-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a5169-112">Command</span></span> | <span data-ttu-id="a5169-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a5169-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a5169-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a5169-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a5169-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="a5169-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a5169-116">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a5169-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a5169-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="a5169-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a5169-118">Nowe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a5169-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="a5169-119">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="a5169-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a5169-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a5169-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a5169-121">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a5169-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="a5169-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a5169-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="a5169-123">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="a5169-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a5169-124">Nowe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="a5169-124">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="a5169-125">Tworzy pomocniczej bazy danych dla istniejącej bazy danych i rozpoczyna się replikacja danych.</span><span class="sxs-lookup"><span data-stu-id="a5169-125">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="a5169-126">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a5169-126">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="a5169-127">Pobiera jeden lub więcej baz danych.</span><span class="sxs-lookup"><span data-stu-id="a5169-127">Gets one or more databases.</span></span> |
| [<span data-ttu-id="a5169-128">Zestaw AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="a5169-128">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="a5169-129">Zmienia pomocniczej bazy danych jako głównej w celu zainicjowania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="a5169-129">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="a5169-130">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="a5169-130">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="a5169-131">Pobiera linki — replikacja geograficzna między bazą danych SQL Azure i grupy zasobów lub SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5169-131">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="a5169-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a5169-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a5169-133">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="a5169-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a5169-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5169-134">Next steps</span></span>

<span data-ttu-id="a5169-135">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a5169-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a5169-136">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a5169-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
