---
title: "aaaAzure PowerShell skryptu — Tworzenie zasad trybu failover bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie bazy danych Azure rozwiązania Cosmos zasad trybu failover"
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
ms.openlocfilehash: 750127385164cd16837b6e29c506d2b44146a629
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-failover-policy-for-high-availability-using-powershell"></a><span data-ttu-id="3ddb6-103">Tworzenie bazy danych Azure rozwiązania Cosmos zasad trybu failover wysokiej dostępności przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ddb6-103">Create an Azure Cosmos DB failover policy for high availability using PowerShell</span></span>

<span data-ttu-id="3ddb6-104">Ten przykładowy skrypt programu PowerShell tworzy zasady trybu failover wysokiej dostępności dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-104">This sample PowerShell script creates a failover policy for high availability for Azure Cosmos DB.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3ddb6-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="3ddb6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Create an Azure Cosmos DB DocumentDB API account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3ddb6-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3ddb6-106">Clean up deployment</span></span>

<span data-ttu-id="3ddb6-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3ddb6-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="3ddb6-108">Script explanation</span></span>

<span data-ttu-id="3ddb6-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-109">This script uses hello following commands.</span></span> <span data-ttu-id="3ddb6-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3ddb6-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="3ddb6-111">Command</span></span> | <span data-ttu-id="3ddb6-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3ddb6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3ddb6-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3ddb6-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="3ddb6-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3ddb6-115">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3ddb6-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="3ddb6-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3ddb6-117">Wywołanie AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="3ddb6-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="3ddb6-118">Wywołuje akcję na hello Azure CosmosDB konta.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="3ddb6-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3ddb6-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="3ddb6-120">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="3ddb6-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3ddb6-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ddb6-121">Next steps</span></span>

<span data-ttu-id="3ddb6-122">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="3ddb6-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="3ddb6-123">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w hello [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3ddb6-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
