---
title: "aaaAzure PowerShell skryptu — Tworzenie konta usługi interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Tworzenie konta usługi interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
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
ms.openlocfilehash: f0751faeca3c1de5906b675e736c58f3d5beaea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="5e667-103">Azure rozwiązania Cosmos bazy danych: Tworzenie konta usługi DocumentDB interfejsu API przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e667-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="5e667-104">Ten przykładowy skrypt programu PowerShell tworzy konto interfejsu API Azure rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e667-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5e667-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5e667-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5e667-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5e667-106">Clean up deployment</span></span>

<span data-ttu-id="5e667-107">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="5e667-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5e667-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5e667-108">Script explanation</span></span>

<span data-ttu-id="5e667-109">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e667-109">This script uses hello following commands.</span></span> <span data-ttu-id="5e667-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5e667-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5e667-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5e667-111">Command</span></span> | <span data-ttu-id="5e667-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5e667-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e667-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e667-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="5e667-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5e667-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e667-115">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5e667-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="5e667-116">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="5e667-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5e667-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e667-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="5e667-118">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5e667-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5e667-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e667-119">Next steps</span></span>

<span data-ttu-id="5e667-120">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="5e667-120">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="5e667-121">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w hello [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5e667-121">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
