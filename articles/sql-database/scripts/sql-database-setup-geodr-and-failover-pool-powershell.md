---
title: "aaaPowerShell przykład aktywny puli replikację geograficzną usługa Azure SQL database | Dokumentacja firmy Microsoft"
description: "Azure PowerShell przykładowy skrypt tooset się aktywna replikacja geograficzna puli bazy danych Azure SQL"
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
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="92f18-103">Użyj programu PowerShell tooconfigure aktywna replikacja geograficzna puli bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="92f18-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="92f18-104">Ten przykładowy skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla bazy danych Azure SQL w puli elastycznej i awaryjnie toohello repliki pomocniczej bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="92f18-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="92f18-105">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="92f18-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="92f18-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="92f18-106">Clean up deployment</span></span>

<span data-ttu-id="92f18-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="92f18-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="92f18-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="92f18-108">Script explanation</span></span>

<span data-ttu-id="92f18-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="92f18-109">This script uses hello following commands.</span></span> <span data-ttu-id="92f18-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="92f18-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="92f18-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="92f18-111">Command</span></span> | <span data-ttu-id="92f18-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="92f18-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="92f18-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="92f18-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="92f18-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="92f18-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="92f18-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="92f18-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="92f18-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="92f18-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="92f18-117">Nowe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="92f18-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="92f18-118">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="92f18-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="92f18-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="92f18-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="92f18-120">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92f18-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="92f18-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="92f18-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="92f18-122">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="92f18-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="92f18-123">Nowe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="92f18-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="92f18-124">Tworzy pomocniczej bazy danych dla istniejącej bazy danych i rozpoczyna się replikacja danych.</span><span class="sxs-lookup"><span data-stu-id="92f18-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="92f18-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="92f18-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="92f18-126">Pobiera jeden lub więcej baz danych.</span><span class="sxs-lookup"><span data-stu-id="92f18-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="92f18-127">Zestaw AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="92f18-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="92f18-128">Zmienia podstawowego toobe dodatkowej bazy danych w tryb failover tooinitiate kolejności.</span><span class="sxs-lookup"><span data-stu-id="92f18-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="92f18-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="92f18-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="92f18-130">Pobiera hello — replikacja geograficzna łącza między bazą danych SQL Azure i grupy zasobów lub SQL Server.</span><span class="sxs-lookup"><span data-stu-id="92f18-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="92f18-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="92f18-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="92f18-132">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="92f18-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="92f18-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92f18-133">Next steps</span></span>

<span data-ttu-id="92f18-134">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="92f18-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="92f18-135">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="92f18-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
