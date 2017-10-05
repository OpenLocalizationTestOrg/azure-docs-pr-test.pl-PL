---
title: "Puli elastycznej bazy danych SQL Azure SQL przykład przenoszenia interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowy skrypt przenieść bazę danych SQL w puli elastycznej SQL"
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
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="01d23-103">Użyj interfejsu wiersza polecenia, aby przenieść bazę danych Azure SQL w puli elastycznej SQL</span><span class="sxs-lookup"><span data-stu-id="01d23-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="01d23-104">Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy dwie pule elastyczne i przenosi bazy danych Azure SQL z jednej puli elastycznej SQL do innej puli elastycznej SQL i przenosi bazy danych z puli elastycznej do poziomu wydajności pojedynczej bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="01d23-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01d23-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="01d23-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="01d23-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="01d23-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="01d23-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01d23-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="01d23-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="01d23-108">Sample script</span></span>

<span data-ttu-id="01d23-109">[!code-azurecli-interactive[główne](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "przeniesienie bazy danych między zestawami")]</span><span class="sxs-lookup"><span data-stu-id="01d23-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="01d23-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="01d23-110">Clean up deployment</span></span>

<span data-ttu-id="01d23-111">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="01d23-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="01d23-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="01d23-112">Script explanation</span></span>

<span data-ttu-id="01d23-113">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="01d23-113">This script uses the following commands.</span></span> <span data-ttu-id="01d23-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="01d23-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01d23-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="01d23-115">Command</span></span> | <span data-ttu-id="01d23-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="01d23-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01d23-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="01d23-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="01d23-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="01d23-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01d23-119">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="01d23-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="01d23-120">Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula.</span><span class="sxs-lookup"><span data-stu-id="01d23-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="01d23-121">Utwórz sql az elastyczna pule</span><span class="sxs-lookup"><span data-stu-id="01d23-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="01d23-122">Tworzy elastycznej puli w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="01d23-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="01d23-123">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="01d23-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="01d23-124">Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01d23-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="01d23-125">Aktualizacja bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="01d23-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="01d23-126">Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne.</span><span class="sxs-lookup"><span data-stu-id="01d23-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="01d23-127">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="01d23-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="01d23-128">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="01d23-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01d23-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01d23-129">Next steps</span></span>

<span data-ttu-id="01d23-130">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01d23-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="01d23-131">Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="01d23-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


