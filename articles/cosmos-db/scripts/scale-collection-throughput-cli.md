---
title: "Przepływność kontenera interfejsu wiersza polecenia skryptu skali Azure rozwiązania Cosmos DB aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - przepływności contianer bazy danych rozwiązania Cosmos Azure skali"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: b1a60feaf43f555a9f6ba20e5e0617f73521c0a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-hello-azure-cli"></a><span data-ttu-id="b9ff7-103">Przepływność kontenera Azure DB rozwiązania Cosmos skali przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b9ff7-103">Scale Azure Cosmos DB container throughput using hello Azure CLI</span></span>

<span data-ttu-id="b9ff7-104">W tym przykładzie skaluje przepływność kontener dla dowolnego rodzaju kontenera Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b9ff7-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b9ff7-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b9ff7-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b9ff7-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b9ff7-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b9ff7-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b9ff7-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b9ff7-109">Clean up deployment</span></span>

<span data-ttu-id="b9ff7-110">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b9ff7-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b9ff7-111">Script explanation</span></span>

<span data-ttu-id="b9ff7-112">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-112">This script uses hello following commands.</span></span> <span data-ttu-id="b9ff7-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b9ff7-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b9ff7-114">Command</span></span> | <span data-ttu-id="b9ff7-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b9ff7-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b9ff7-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="b9ff7-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b9ff7-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b9ff7-118">AZ cosmosdb aktualizacji</span><span class="sxs-lookup"><span data-stu-id="b9ff7-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="b9ff7-119">Aktualizuje konto bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="b9ff7-120">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="b9ff7-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b9ff7-121">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b9ff7-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9ff7-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b9ff7-122">Next steps</span></span>

<span data-ttu-id="b9ff7-123">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9ff7-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b9ff7-124">Dodatkowe przykłady skryptów wiersza polecenia platformy Azure rozwiązania Cosmos bazy danych można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure rozwiązania Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b9ff7-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
