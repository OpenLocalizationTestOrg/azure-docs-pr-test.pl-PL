---
title: "Baza danych Azure SQL przykład monitora skali — pojedynczy aaaCLI | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowy skrypt toomonitor i skalowania pojedynczej bazy danych Azure SQL"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="6d87d-103">Użyj interfejsu wiersza polecenia toomonitor i skalowania pojedynczej bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="6d87d-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="6d87d-104">Ten przykładowy skrypt wiersza polecenia platformy Azure skaluje jeden poziom wydajności różnych tooa bazy danych Azure SQL po podczas badania informacji o rozmiarze hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d87d-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6d87d-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6d87d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6d87d-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="6d87d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6d87d-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6d87d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6d87d-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6d87d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6d87d-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6d87d-109">Clean up deployment</span></span>

<span data-ttu-id="6d87d-110">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="6d87d-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6d87d-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6d87d-111">Script explanation</span></span>

<span data-ttu-id="6d87d-112">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="6d87d-112">This script uses hello following commands.</span></span> <span data-ttu-id="6d87d-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="6d87d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6d87d-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6d87d-114">Command</span></span> | <span data-ttu-id="6d87d-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6d87d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d87d-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6d87d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6d87d-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6d87d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d87d-118">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="6d87d-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="6d87d-119">Tworzy serwer logiczny, który jest hostem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d87d-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="6d87d-120">bazy danych sql az Pokaż — użycie</span><span class="sxs-lookup"><span data-stu-id="6d87d-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="6d87d-121">Przedstawia informacje o użycia rozmiar hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d87d-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="6d87d-122">Aktualizacja bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="6d87d-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="6d87d-123">Aktualizuje właściwości bazy danych (na przykład hello usługi warstwy poziomu) lub przenosi bazy danych do z lub między elastyczne pule.</span><span class="sxs-lookup"><span data-stu-id="6d87d-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="6d87d-124">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="6d87d-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d87d-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6d87d-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="6d87d-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d87d-126">Next steps</span></span>

<span data-ttu-id="6d87d-127">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d87d-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d87d-128">Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6d87d-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
