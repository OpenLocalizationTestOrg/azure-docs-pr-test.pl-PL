---
title: AAA "Azure CLI Azure skali skryptu bazy danych PostgreSQL | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie usługi Azure CLI - bazą danych Azure skalowania dla poziom wydajności różnych tooa PostgreSQL serwera po zapytań hello metryki."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="d3268-103">Monitorowanie i skalować pojedynczy serwer PostgreSQL przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d3268-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="d3268-104">Ten przykładowy skrypt CLI skaluje pojedynczej bazy danych Azure na poziomie wydajności różnych tooa serwera PostgreSQL po zapytań hello metryki.</span><span class="sxs-lookup"><span data-stu-id="d3268-104">This sample CLI script scales a single Azure Database for PostgreSQL server tooa different performance level after querying hello metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d3268-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d3268-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d3268-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="d3268-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d3268-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d3268-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d3268-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d3268-108">Sample script</span></span>
<span data-ttu-id="d3268-109">W ten przykładowy skrypt zmienić hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="d3268-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="d3268-110">Zastąp identyfikator subskrypcji hello używane w poleceniach monitor az hello z identyfikatorem subskrypcji.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="d3268-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d3268-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d3268-111">Clean up deployment</span></span>
<span data-ttu-id="d3268-112">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="d3268-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="d3268-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d3268-113">Script explanation</span></span>
<span data-ttu-id="d3268-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="d3268-114">This script uses hello following commands.</span></span> <span data-ttu-id="d3268-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d3268-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d3268-116">**Polecenie**</span><span class="sxs-lookup"><span data-stu-id="d3268-116">**Command**</span></span> | <span data-ttu-id="d3268-117">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="d3268-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="d3268-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d3268-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d3268-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d3268-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d3268-120">utworzenie przez serwer postgres az</span><span class="sxs-lookup"><span data-stu-id="d3268-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="d3268-121">Tworzy serwer PostgreSQL obsługującego hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="d3268-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="d3268-122">Lista metryki monitor az</span><span class="sxs-lookup"><span data-stu-id="d3268-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="d3268-123">Wyświetl listę hello wartość metryki hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3268-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="d3268-124">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="d3268-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d3268-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3268-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3268-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3268-126">Next steps</span></span>
- <span data-ttu-id="d3268-127">Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="d3268-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="d3268-128">Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d3268-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="d3268-129">Przeczytaj więcej na temat skalowania: [warstwy usług](../concepts-service-tiers.md) i [obliczeniowe i jednostek magazynu](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d3268-129">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
