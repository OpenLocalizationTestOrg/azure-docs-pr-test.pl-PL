---
title: "aaaPowerShell przykład import-pliku bacpac plików Azure SQL database | Dokumentacja firmy Microsoft"
description: "Azure PowerShell przykładowy skrypt tooimport pliku bacpac Kafelek do bazy danych SQL"
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="fc5f2-103">Za pomocą programu PowerShell tooimport pliku bacpac pliku do bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="fc5f2-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="fc5f2-104">Ten przykładowy skrypt programu PowerShell importuje bazę danych z **pliku bacpac** pliku do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="fc5f2-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="fc5f2-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fc5f2-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="fc5f2-106">Clean up deployment</span></span>

<span data-ttu-id="fc5f2-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fc5f2-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="fc5f2-108">Script explanation</span></span>

<span data-ttu-id="fc5f2-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-109">This script uses hello following commands.</span></span> <span data-ttu-id="fc5f2-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fc5f2-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="fc5f2-111">Command</span></span> | <span data-ttu-id="fc5f2-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fc5f2-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc5f2-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fc5f2-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fc5f2-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc5f2-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="fc5f2-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fc5f2-116">Tworzy serwer logiczny, że hosty hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="fc5f2-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="fc5f2-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="fc5f2-118">Tworzy zapory reguły tooallow dostępu tooall baz danych na serwerze hello z zakresu adresów IP hello wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="fc5f2-119">Nowe AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="fc5f2-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="fc5f2-120">Importy a bacpac plików i utworzyć nową bazę danych na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="fc5f2-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fc5f2-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fc5f2-122">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc5f2-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc5f2-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc5f2-123">Next steps</span></span>

<span data-ttu-id="fc5f2-124">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc5f2-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fc5f2-125">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f2-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
