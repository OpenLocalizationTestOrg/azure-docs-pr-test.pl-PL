---
title: "Parametry połączenia bazy danych programu PowerShell Get skryptu Azure rozwiązania Cosmos dla aplikacji bazy danych MongoDB aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — parametry połączenia bazy danych rozwiązania Cosmos Azure Get dla aplikacji bazy danych MongoDB"
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
ms.openlocfilehash: d04502b8f59bb6f3cb8bec696595f962b479fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="55cea-103">Pobierz ciąg połączenia bazy danych rozwiązania Cosmos Azure dla aplikacji bazy danych MongoDB przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="55cea-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="55cea-104">W tym przykładzie pobiera parametry połączenia bazy danych rozwiązania Cosmos Azure dla aplikacji bazy danych MongoDB przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55cea-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="55cea-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="55cea-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get hello MongoDB connection string from an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="55cea-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="55cea-106">Clean up deployment</span></span>

<span data-ttu-id="55cea-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="55cea-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="55cea-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="55cea-108">Script explanation</span></span>

<span data-ttu-id="55cea-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="55cea-109">This script uses hello following commands.</span></span> <span data-ttu-id="55cea-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="55cea-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="55cea-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="55cea-111">Command</span></span> | <span data-ttu-id="55cea-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="55cea-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55cea-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="55cea-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="55cea-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="55cea-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55cea-115">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="55cea-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="55cea-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="55cea-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="55cea-117">Wywołanie AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="55cea-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="55cea-118">Wywołuje akcję na hello Azure CosmosDB konta.</span><span class="sxs-lookup"><span data-stu-id="55cea-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="55cea-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="55cea-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="55cea-120">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="55cea-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="55cea-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55cea-121">Next steps</span></span>

<span data-ttu-id="55cea-122">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="55cea-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="55cea-123">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w hello [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="55cea-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
