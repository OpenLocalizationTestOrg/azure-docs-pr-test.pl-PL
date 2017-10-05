---
title: "Azure skrypt programu PowerShell-Multiregion replikację bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3a469ba43e6c601f5eb0e13d588cd0bd4a0f8683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="db8de-103">Replikację bazy danych Azure rozwiązania Cosmos konta bazy danych w wielu regionach i skonfiguruj priorytetów trybu failover przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="db8de-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="db8de-104">W tym przykładzie jest dowolne konto bazy danych Azure DB rozwiązania Cosmos w wielu regionach i konfiguruje priorytetów trybu failover przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db8de-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="db8de-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="db8de-105">Sample script</span></span>

<span data-ttu-id="db8de-106">[!code-powershell[główne](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "replikację konta bazy danych Azure rozwiązania Cosmos w różnych regionach")]</span><span class="sxs-lookup"><span data-stu-id="db8de-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="db8de-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="db8de-107">Clean up deployment</span></span>

<span data-ttu-id="db8de-108">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="db8de-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="db8de-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="db8de-109">Script explanation</span></span>

<span data-ttu-id="db8de-110">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="db8de-110">This script uses the following commands.</span></span> <span data-ttu-id="db8de-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="db8de-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="db8de-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="db8de-112">Command</span></span> | <span data-ttu-id="db8de-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="db8de-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="db8de-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="db8de-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="db8de-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="db8de-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="db8de-116">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="db8de-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="db8de-117">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="db8de-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="db8de-118">Zestaw AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="db8de-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="db8de-119">Modyfikuje konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="db8de-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="db8de-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="db8de-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="db8de-121">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="db8de-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="db8de-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db8de-122">Next steps</span></span>

<span data-ttu-id="db8de-123">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="db8de-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="db8de-124">Dodatkowe przykłady skryptów PowerShell DB rozwiązania Cosmos Azure można znaleźć w [skryptów programu PowerShell DB rozwiązania Cosmos Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="db8de-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>