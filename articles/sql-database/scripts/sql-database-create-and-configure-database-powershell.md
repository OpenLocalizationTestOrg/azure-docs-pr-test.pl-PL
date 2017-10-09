---
title: "aaaPowerShell przykład — tworzenie bazy danych Azure SQL | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toocreate bazy danych Azure SQL Azure PowerShell"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="d533a-103">Użyj programu PowerShell toocreate pojedynczej bazy danych Azure SQL i skonfiguruj regułę zapory</span><span class="sxs-lookup"><span data-stu-id="d533a-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="d533a-104">Ten przykładowy skrypt programu PowerShell tworzy bazę danych Azure SQL i konfiguruje regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="d533a-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="d533a-105">Po pomyślnym uruchomieniu skryptu hello powitalne bazy danych SQL miała dostęp do wszystkich usług platformy Azure i hello skonfigurowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="d533a-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d533a-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d533a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d533a-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d533a-107">Clean up deployment</span></span>

<span data-ttu-id="d533a-108">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="d533a-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d533a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d533a-109">Script explanation</span></span>

<span data-ttu-id="d533a-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="d533a-110">This script uses hello following commands.</span></span> <span data-ttu-id="d533a-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d533a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d533a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d533a-112">Command</span></span> | <span data-ttu-id="d533a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d533a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d533a-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d533a-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d533a-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d533a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d533a-116">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="d533a-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d533a-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="d533a-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d533a-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="d533a-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="d533a-119">Tworzy zapory reguły tooallow dostępu tooall baz danych na serwerze hello z zakresu adresów IP hello wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="d533a-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="d533a-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d533a-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="d533a-121">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d533a-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="d533a-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d533a-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d533a-123">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d533a-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d533a-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d533a-124">Next steps</span></span>

<span data-ttu-id="d533a-125">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d533a-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d533a-126">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d533a-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



