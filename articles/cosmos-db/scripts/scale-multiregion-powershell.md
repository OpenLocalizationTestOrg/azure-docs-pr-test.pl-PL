---
title: "Skrypt programu PowerShell-Multiregion aaaAzure replikacji dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - Multiregion replikacji dla bazy danych Azure rozwiązania Cosmos"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 8e3e79f086f46fc037d52589eb8bcf4557214566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="35bba-103">Replikację bazy danych Azure rozwiązania Cosmos konta bazy danych w wielu regionach i skonfiguruj priorytetów trybu failover przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="35bba-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="35bba-104">W tym przykładzie jest dowolne konto bazy danych Azure DB rozwiązania Cosmos w wielu regionach i konfiguruje priorytetów trybu failover przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35bba-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="35bba-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="35bba-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="35bba-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="35bba-106">Clean up deployment</span></span>

<span data-ttu-id="35bba-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="35bba-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="35bba-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="35bba-108">Script explanation</span></span>

<span data-ttu-id="35bba-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="35bba-109">This script uses hello following commands.</span></span> <span data-ttu-id="35bba-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="35bba-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="35bba-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="35bba-111">Command</span></span> | <span data-ttu-id="35bba-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="35bba-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35bba-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35bba-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="35bba-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="35bba-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35bba-115">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="35bba-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="35bba-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="35bba-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="35bba-117">Zestaw AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="35bba-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="35bba-118">Modyfikuje hello konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="35bba-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="35bba-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35bba-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="35bba-120">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="35bba-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="35bba-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35bba-121">Next steps</span></span>

<span data-ttu-id="35bba-122">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="35bba-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="35bba-123">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w hello [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="35bba-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
