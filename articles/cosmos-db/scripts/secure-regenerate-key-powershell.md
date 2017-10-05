---
title: "Klucz konta w usłudze Azure DB rozwiązania Cosmos Azure Regenerate skrypt programu PowerShell | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - klucz konta bazy danych rozwiązania Cosmos Regenerate Azure"
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
ms.openlocfilehash: 187d7b0839e1cd94122d4455c11eda05673f5acc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-powershell"></a><span data-ttu-id="2e61a-103">Ponowne generowanie klucza konta bazy danych rozwiązania Cosmos Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e61a-103">Regenerate an Azure Cosmos DB account key using PowerShell</span></span>

<span data-ttu-id="2e61a-104">W tym przykładzie generuje dowolnego rodzaju klucz konta bazy danych Azure rozwiązania Cosmos przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2e61a-104">This sample regenerates any kind of Azure Cosmos DB account key using the Azure CLI.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2e61a-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="2e61a-105">Sample script</span></span>

<span data-ttu-id="2e61a-106">[!code-powershell[główne](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "klucze konta ponownie wygenerować rozwiązania Cosmos bazy danych Azure")]</span><span class="sxs-lookup"><span data-stu-id="2e61a-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "Regenerate Azure Cosmos DB account keys")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2e61a-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="2e61a-107">Clean up deployment</span></span>

<span data-ttu-id="2e61a-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="2e61a-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2e61a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="2e61a-109">Script explanation</span></span>

<span data-ttu-id="2e61a-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="2e61a-110">This script uses the following commands.</span></span> <span data-ttu-id="2e61a-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e61a-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2e61a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="2e61a-112">Command</span></span> | <span data-ttu-id="2e61a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2e61a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e61a-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2e61a-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="2e61a-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="2e61a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2e61a-116">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2e61a-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="2e61a-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="2e61a-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2e61a-118">Wywołanie AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="2e61a-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="2e61a-119">Wywołuje akcję na konto Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="2e61a-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="2e61a-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2e61a-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="2e61a-121">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="2e61a-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2e61a-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e61a-122">Next steps</span></span>

<span data-ttu-id="2e61a-123">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="2e61a-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="2e61a-124">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2e61a-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>