---
title: "przykład inspekcji zagrożenie aaaPowerShell wykrywania Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Azure PowerShell przykładowy skrypt tooconfigure Inspekcja i wykrywanie zagrożeń w bazie danych SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="95d7e-103">Użyj programu PowerShell tooconfigure bazy danych SQL inspekcji i wykrywania zagrożeń</span><span class="sxs-lookup"><span data-stu-id="95d7e-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="95d7e-104">Ten przykładowy skrypt programu PowerShell konfiguruje bazę danych SQL inspekcji i wykrywania zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="95d7e-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="95d7e-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="95d7e-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="95d7e-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="95d7e-106">Clean up deployment</span></span>

<span data-ttu-id="95d7e-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="95d7e-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="95d7e-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="95d7e-108">Script explanation</span></span>

<span data-ttu-id="95d7e-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="95d7e-109">This script uses hello following commands.</span></span> <span data-ttu-id="95d7e-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="95d7e-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="95d7e-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="95d7e-111">Command</span></span> | <span data-ttu-id="95d7e-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="95d7e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="95d7e-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="95d7e-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="95d7e-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="95d7e-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="95d7e-115">Nowe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="95d7e-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="95d7e-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="95d7e-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="95d7e-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="95d7e-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="95d7e-118">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="95d7e-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="95d7e-119">Nowe AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="95d7e-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="95d7e-120">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="95d7e-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="95d7e-121">Zestaw AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="95d7e-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="95d7e-122">Ustawia hello zasad inspekcji dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="95d7e-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="95d7e-123">Zestaw AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="95d7e-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="95d7e-124">Ustawia zasady wykrywania zagrożeń w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="95d7e-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="95d7e-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="95d7e-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="95d7e-126">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="95d7e-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="95d7e-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95d7e-127">Next steps</span></span>

<span data-ttu-id="95d7e-128">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="95d7e-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="95d7e-129">Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w hello [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="95d7e-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
