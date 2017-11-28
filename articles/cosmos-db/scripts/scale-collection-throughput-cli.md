---
title: "Przepływności kontenera w usłudze Azure DB rozwiązania Cosmos Azure skali skryptu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="95a5a-103">Przepływność kontenera Azure DB rozwiązania Cosmos skali przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="95a5a-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="95a5a-104">W tym przykładzie skaluje przepływność kontener dla dowolnego rodzaju kontenera Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="95a5a-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="95a5a-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="95a5a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="95a5a-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="95a5a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="95a5a-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="95a5a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="95a5a-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="95a5a-108">Sample script</span></span>

<span data-ttu-id="95a5a-109">[!code-azurecli-interactive[główne](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "przepływności bazy danych rozwiązania Cosmos Azure skali")]</span><span class="sxs-lookup"><span data-stu-id="95a5a-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="95a5a-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="95a5a-110">Clean up deployment</span></span>

<span data-ttu-id="95a5a-111">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="95a5a-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="95a5a-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="95a5a-112">Script explanation</span></span>

<span data-ttu-id="95a5a-113">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="95a5a-113">This script uses the following commands.</span></span> <span data-ttu-id="95a5a-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="95a5a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="95a5a-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="95a5a-115">Command</span></span> | <span data-ttu-id="95a5a-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="95a5a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="95a5a-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="95a5a-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="95a5a-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="95a5a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="95a5a-119">AZ cosmosdb aktualizacji</span><span class="sxs-lookup"><span data-stu-id="95a5a-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="95a5a-120">Aktualizuje konto bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="95a5a-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="95a5a-121">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="95a5a-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="95a5a-122">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="95a5a-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="95a5a-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95a5a-123">Next steps</span></span>

<span data-ttu-id="95a5a-124">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="95a5a-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="95a5a-125">Dodatkowe przykłady skryptów wiersza polecenia platformy Azure rozwiązania Cosmos bazy danych można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure rozwiązania Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="95a5a-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
