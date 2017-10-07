---
title: "aaaCLI przykład — tworzenie bazy danych Azure SQL | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toocreate bazy danych SQL Azure CLI"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="90a22-103">Użyj interfejsu wiersza polecenia toocreate pojedynczej bazy danych Azure SQL i skonfiguruj regułę zapory</span><span class="sxs-lookup"><span data-stu-id="90a22-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="90a22-104">W tym przykładzie skrypt wiersza polecenia platformy Azure utworzy bazę danych Azure SQL i skonfigurować regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="90a22-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="90a22-105">Po pomyślnym uruchomieniu skryptu hello powitalne bazy danych SQL miała dostęp do wszystkich usług platformy Azure i hello skonfigurowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="90a22-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="90a22-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="90a22-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="90a22-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="90a22-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="90a22-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="90a22-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="90a22-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="90a22-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="90a22-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="90a22-110">Clean up deployment</span></span>

<span data-ttu-id="90a22-111">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="90a22-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="90a22-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="90a22-112">Script explanation</span></span>

<span data-ttu-id="90a22-113">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="90a22-113">This script uses hello following commands.</span></span> <span data-ttu-id="90a22-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="90a22-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="90a22-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="90a22-115">Command</span></span> | <span data-ttu-id="90a22-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="90a22-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="90a22-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="90a22-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="90a22-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="90a22-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="90a22-119">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="90a22-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="90a22-120">Tworzy serwer logiczny, że hosty hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="90a22-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="90a22-121">Utwórz zapory serwera sql az</span><span class="sxs-lookup"><span data-stu-id="90a22-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="90a22-122">Tworzy zapory reguły tooallow dostępu tooall baz danych na serwerze hello z zakresu adresów IP hello wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="90a22-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="90a22-123">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="90a22-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="90a22-124">Tworzy hello bazy danych SQL w powitania serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="90a22-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="90a22-125">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="90a22-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="90a22-126">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="90a22-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="90a22-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90a22-127">Next steps</span></span>

<span data-ttu-id="90a22-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="90a22-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="90a22-129">Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="90a22-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

