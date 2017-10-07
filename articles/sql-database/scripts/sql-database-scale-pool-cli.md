---
title: "przykład aaaCLI skaluje elastycznej puli Azure SQL bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowy skrypt tooscale puli elastycznej SQL w bazie danych SQL Azure"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="78b38-103">Użyj interfejsu wiersza polecenia tooscale puli elastycznej SQL w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="78b38-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="78b38-104">Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy pule elastyczne SQL, przenosi puli baz danych, a następnie zmienia poziomy wydajności puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="78b38-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="78b38-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="78b38-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="78b38-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="78b38-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="78b38-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="78b38-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="78b38-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="78b38-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="78b38-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="78b38-109">Clean up deployment</span></span>

<span data-ttu-id="78b38-110">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="78b38-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="78b38-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="78b38-111">Script explanation</span></span>

<span data-ttu-id="78b38-112">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, serwera logicznego bazy danych SQL i reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="78b38-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="78b38-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="78b38-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="78b38-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="78b38-114">Command</span></span> | <span data-ttu-id="78b38-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="78b38-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="78b38-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="78b38-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="78b38-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="78b38-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="78b38-118">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="78b38-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="78b38-119">Tworzy serwer logiczny, że hosty hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="78b38-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="78b38-120">Utwórz sql az elastyczna pule</span><span class="sxs-lookup"><span data-stu-id="78b38-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="78b38-121">Tworzy elastycznej puli baz danych w ramach powitania serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="78b38-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="78b38-122">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="78b38-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="78b38-123">Tworzy hello bazy danych SQL w powitania serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="78b38-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="78b38-124">Aktualizacja pule elastyczne sql az</span><span class="sxs-lookup"><span data-stu-id="78b38-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="78b38-125">Aktualizuje elastycznej puli baz danych, w tym hello zmiany przykład przypisane eDTU.</span><span class="sxs-lookup"><span data-stu-id="78b38-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="78b38-126">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="78b38-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="78b38-127">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="78b38-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="78b38-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78b38-128">Next steps</span></span>

<span data-ttu-id="78b38-129">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="78b38-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="78b38-130">Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="78b38-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
