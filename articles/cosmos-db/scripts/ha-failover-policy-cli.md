---
title: "Azure CLI skryptu-Tworzenie zasad trybu failover wysokiej dostępności | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie zasad trybu failover wysokiej dostępności"
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
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="adc56-103">Tworzenie zasad trybu failover wysokiej dostępności przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="adc56-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="adc56-104">Ten przykładowy skrypt interfejsu wiersza polecenia tworzy konto bazy danych rozwiązania Cosmos Azure, a następnie konfiguruje wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="adc56-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="adc56-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="adc56-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="adc56-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="adc56-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="adc56-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="adc56-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="adc56-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="adc56-108">Sample script</span></span>

<span data-ttu-id="adc56-109">[!code-azurecli-interactive[główne](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "tworzenie bazy danych Azure rozwiązania Cosmos zasad trybu failover")]</span><span class="sxs-lookup"><span data-stu-id="adc56-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="adc56-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="adc56-110">Clean up deployment</span></span>

<span data-ttu-id="adc56-111">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="adc56-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="adc56-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="adc56-112">Script explanation</span></span>

<span data-ttu-id="adc56-113">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="adc56-113">This script uses the following commands.</span></span> <span data-ttu-id="adc56-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="adc56-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="adc56-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="adc56-115">Command</span></span> | <span data-ttu-id="adc56-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="adc56-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="adc56-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="adc56-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="adc56-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="adc56-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="adc56-119">Utwórz az cosmosdb</span><span class="sxs-lookup"><span data-stu-id="adc56-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="adc56-120">Tworzy konto bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="adc56-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="adc56-121">AZ cosmosdb aktualizacji</span><span class="sxs-lookup"><span data-stu-id="adc56-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="adc56-122">Aktualizuje konto bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="adc56-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="adc56-123">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="adc56-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="adc56-124">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="adc56-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="adc56-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="adc56-125">Next steps</span></span>

<span data-ttu-id="adc56-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="adc56-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="adc56-127">Dodatkowe przykłady skryptów wiersza polecenia platformy Azure rozwiązania Cosmos bazy danych można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure rozwiązania Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="adc56-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
