---
title: "Azure CLI skryptu-tworzenie zapory na potrzeby bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — utworzenie zapory dla bazy danych Azure rozwiązania Cosmos"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 51f61901e1b1615e48582690dea701a01a56ebca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-the-azure-cli"></a><span data-ttu-id="4f1a2-103">Azure DB rozwiązania Cosmos: Utworzenie zapory przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4f1a2-103">Azure Cosmos DB: Create a firewall using the Azure CLI</span></span>

<span data-ttu-id="4f1a2-104">Ten przykładowy skrypt CLI tworzy zasady zapory dla każdego typu konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4f1a2-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4f1a2-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="4f1a2-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4f1a2-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4f1a2-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="4f1a2-108">Sample script</span></span>

<span data-ttu-id="4f1a2-109">[!code-azurecli-interactive[główne](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "utworzyć zapory bazy danych Azure rozwiązania Cosmos")]</span><span class="sxs-lookup"><span data-stu-id="4f1a2-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4f1a2-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4f1a2-110">Clean up deployment</span></span>

<span data-ttu-id="4f1a2-111">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4f1a2-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="4f1a2-112">Script explanation</span></span>

<span data-ttu-id="4f1a2-113">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-113">This script uses the following commands.</span></span> <span data-ttu-id="4f1a2-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4f1a2-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="4f1a2-115">Command</span></span> | <span data-ttu-id="4f1a2-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4f1a2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4f1a2-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="4f1a2-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4f1a2-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4f1a2-119">Utwórz az cosmosdb</span><span class="sxs-lookup"><span data-stu-id="4f1a2-119">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="4f1a2-120">Tworzy konto Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-120">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="4f1a2-121">AZ cosmosdb aktualizacji</span><span class="sxs-lookup"><span data-stu-id="4f1a2-121">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="4f1a2-122">Aktualizuje konto Azure CosmosDB do uwzględnienia ustawień zapory.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-122">Updates an Azure CosmosDB account to include firewall settings.</span></span> |
| [<span data-ttu-id="4f1a2-123">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="4f1a2-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="4f1a2-124">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f1a2-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4f1a2-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f1a2-125">Next steps</span></span>

<span data-ttu-id="4f1a2-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4f1a2-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4f1a2-127">Dodatkowe przykłady skryptów wiersza polecenia platformy Azure rozwiązania Cosmos bazy danych można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure rozwiązania Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4f1a2-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
