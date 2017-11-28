---
title: "Azure PowerShell skryptu-tworzenie zapory na potrzeby bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — utworzenie zapory dla bazy danych Azure rozwiązania Cosmos"
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="b4f8d-103">Azure DB rozwiązania Cosmos: Utworzenie zapory przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4f8d-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="b4f8d-104">Ten przykładowy skrypt programu PowerShell tworzy zapory dla dowolnego rodzaju konto interfejsu API Azure rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b4f8d-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b4f8d-105">Sample script</span></span>

<span data-ttu-id="b4f8d-106">[!code-powershell[główne](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "utworzenie zapory dla bazy danych Azure rozwiązania Cosmos")]</span><span class="sxs-lookup"><span data-stu-id="b4f8d-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b4f8d-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b4f8d-107">Clean up deployment</span></span>

<span data-ttu-id="b4f8d-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b4f8d-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b4f8d-109">Script explanation</span></span>

<span data-ttu-id="b4f8d-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-110">This script uses the following commands.</span></span> <span data-ttu-id="b4f8d-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b4f8d-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b4f8d-112">Command</span></span> | <span data-ttu-id="b4f8d-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b4f8d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4f8d-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4f8d-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="b4f8d-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4f8d-116">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b4f8d-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="b4f8d-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b4f8d-118">Zestaw AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="b4f8d-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="b4f8d-119">Modyfikuje konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="b4f8d-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4f8d-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="b4f8d-121">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b4f8d-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b4f8d-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4f8d-122">Next steps</span></span>

<span data-ttu-id="b4f8d-123">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="b4f8d-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="b4f8d-124">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b4f8d-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>