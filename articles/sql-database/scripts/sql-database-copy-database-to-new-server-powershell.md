---
title: "Przykład kopii Azure PowerShell SQL server Nowa baza danych | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell można skopiować do nowego serwera bazy danych SQL"
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
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="da8ad-103">Aby skopiować do nowego serwera bazy danych SQL za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="da8ad-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="da8ad-104">Ten przykładowy skrypt programu PowerShell tworzy kopię istniejącej bazy danych w nowym serwerze.</span><span class="sxs-lookup"><span data-stu-id="da8ad-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="da8ad-105">Kopiowanie bazy danych do nowego serwera</span><span class="sxs-lookup"><span data-stu-id="da8ad-105">Copy a database to a new server</span></span>

<span data-ttu-id="da8ad-106">[!code-powershell[główne](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "kopii bazy danych, do nowego serwera")]</span><span class="sxs-lookup"><span data-stu-id="da8ad-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="da8ad-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="da8ad-107">Clean up deployment</span></span>

<span data-ttu-id="da8ad-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="da8ad-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="da8ad-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="da8ad-109">Script explanation</span></span>

<span data-ttu-id="da8ad-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="da8ad-110">This script uses the following commands.</span></span> <span data-ttu-id="da8ad-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="da8ad-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="da8ad-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="da8ad-112">Command</span></span> | <span data-ttu-id="da8ad-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="da8ad-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="da8ad-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="da8ad-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="da8ad-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="da8ad-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="da8ad-116">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="da8ad-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="da8ad-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="da8ad-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="da8ad-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="da8ad-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="da8ad-119">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="da8ad-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="da8ad-120">Nowe AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="da8ad-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="da8ad-121">Tworzy kopię bazy danych, który używa migawki w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="da8ad-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="da8ad-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="da8ad-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="da8ad-123">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="da8ad-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="da8ad-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da8ad-124">Next steps</span></span>

<span data-ttu-id="da8ad-125">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da8ad-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="da8ad-126">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="da8ad-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
