---
title: "puli elastycznej bazy danych SQL Azure SQL przenoszenia przykład aaaCLI | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toomove bazy danych SQL w puli elastycznej SQL Azure CLI"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="88d5f-103">Użyj interfejsu wiersza polecenia toomove bazy danych Azure SQL w puli elastycznej SQL</span><span class="sxs-lookup"><span data-stu-id="88d5f-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="88d5f-104">Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy dwie pule elastyczne i przenosi bazy danych Azure SQL z jednej puli elastycznej SQL do innej puli elastycznej SQL i przenosi hello bazy danych poza poziom wydajności pojedynczej bazy danych Azure tooa puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="88d5f-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="88d5f-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="88d5f-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="88d5f-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="88d5f-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="88d5f-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88d5f-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="88d5f-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="88d5f-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="88d5f-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="88d5f-109">Clean up deployment</span></span>

<span data-ttu-id="88d5f-110">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="88d5f-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="88d5f-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="88d5f-111">Script explanation</span></span>

<span data-ttu-id="88d5f-112">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="88d5f-112">This script uses hello following commands.</span></span> <span data-ttu-id="88d5f-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="88d5f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="88d5f-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="88d5f-114">Command</span></span> | <span data-ttu-id="88d5f-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="88d5f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="88d5f-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="88d5f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="88d5f-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="88d5f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="88d5f-118">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="88d5f-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="88d5f-119">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="88d5f-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="88d5f-120">Utwórz sql az elastyczna pule</span><span class="sxs-lookup"><span data-stu-id="88d5f-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="88d5f-121">Tworzy elastycznej puli w ramach powitania serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="88d5f-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="88d5f-122">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="88d5f-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="88d5f-123">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="88d5f-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="88d5f-124">Aktualizacja bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="88d5f-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="88d5f-125">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="88d5f-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="88d5f-126">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="88d5f-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="88d5f-127">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="88d5f-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="88d5f-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88d5f-128">Next steps</span></span>

<span data-ttu-id="88d5f-129">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88d5f-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="88d5f-130">Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="88d5f-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


