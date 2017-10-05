---
title: "Przykład CLI skaluje elastycznej puli Azure SQL bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowy skrypt do skalowania puli elastycznej SQL w bazie danych SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="9666f-103">Użyj interfejsu wiersza polecenia, aby skalować puli elastycznej SQL w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9666f-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="9666f-104">Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy pule elastyczne SQL, przenosi puli baz danych, a następnie zmienia poziomy wydajności puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="9666f-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9666f-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9666f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9666f-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="9666f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="9666f-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9666f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9666f-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9666f-108">Sample script</span></span>

<span data-ttu-id="9666f-109">[!code-azurecli-interactive[główne](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "przeniesienie bazy danych między zestawami")]</span><span class="sxs-lookup"><span data-stu-id="9666f-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9666f-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9666f-110">Clean up deployment</span></span>

<span data-ttu-id="9666f-111">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="9666f-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9666f-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9666f-112">Script explanation</span></span>

<span data-ttu-id="9666f-113">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, serwera logicznego bazy danych SQL i reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="9666f-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="9666f-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9666f-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9666f-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9666f-115">Command</span></span> | <span data-ttu-id="9666f-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9666f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9666f-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9666f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9666f-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9666f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9666f-119">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="9666f-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="9666f-120">Tworzy serwer logiczny, który jest hostem bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9666f-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="9666f-121">Utwórz sql az elastyczna pule</span><span class="sxs-lookup"><span data-stu-id="9666f-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="9666f-122">Tworzy elastycznej puli baz danych w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="9666f-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="9666f-123">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="9666f-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="9666f-124">Tworzy bazę danych SQL w serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="9666f-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="9666f-125">Aktualizacja pule elastyczne sql az</span><span class="sxs-lookup"><span data-stu-id="9666f-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="9666f-126">Aktualizuje elastycznej puli baz danych, w tym przykładzie zmiany przypisane eDTU.</span><span class="sxs-lookup"><span data-stu-id="9666f-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="9666f-127">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="9666f-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9666f-128">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9666f-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9666f-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9666f-129">Next steps</span></span>

<span data-ttu-id="9666f-130">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9666f-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9666f-131">Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9666f-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
