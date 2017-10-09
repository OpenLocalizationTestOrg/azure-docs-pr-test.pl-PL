---
title: "aaaAzure CLI przykłady tooscale Azure bazy danych serwera MySQL | Dokumentacja firmy Microsoft"
description: "Ten przykładowy skrypt interfejsu wiersza polecenia skaluje bazy danych Azure na poziomie wydajności różnych tooa serwera MySQL po zapytań hello metryki."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="f7e1a-103">Monitorowanie i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f7e1a-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="f7e1a-104">Ten przykładowy skrypt interfejsu wiersza polecenia skaluje pojedynczej bazy danych Azure na poziomie wydajności różnych tooa serwera MySQL po zapytań hello metryki.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f7e1a-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f7e1a-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f7e1a-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f7e1a-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f7e1a-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f7e1a-108">Sample script</span></span>
<span data-ttu-id="f7e1a-109">W ten przykładowy skrypt zmienić hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="f7e1a-110">Zastąp identyfikator subskrypcji hello używane w poleceniach monitor az hello z identyfikatorem subskrypcji.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="f7e1a-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f7e1a-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f7e1a-111">Clean up deployment</span></span>
<span data-ttu-id="f7e1a-112">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="f7e1a-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f7e1a-113">Script explanation</span></span>
<span data-ttu-id="f7e1a-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-114">This script uses hello following commands.</span></span> <span data-ttu-id="f7e1a-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f7e1a-116">**Polecenie**</span><span class="sxs-lookup"><span data-stu-id="f7e1a-116">**Command**</span></span> | <span data-ttu-id="f7e1a-117">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="f7e1a-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="f7e1a-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f7e1a-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="f7e1a-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f7e1a-120">utworzenie przez serwer mysql az</span><span class="sxs-lookup"><span data-stu-id="f7e1a-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="f7e1a-121">Tworzy serwer MySQL obsługującego hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="f7e1a-122">Lista metryki monitor az</span><span class="sxs-lookup"><span data-stu-id="f7e1a-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="f7e1a-123">Wyświetl listę hello wartość metryki hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="f7e1a-124">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="f7e1a-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="f7e1a-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f7e1a-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f7e1a-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7e1a-126">Next steps</span></span>
- <span data-ttu-id="f7e1a-127">Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f7e1a-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="f7e1a-128">Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f7e1a-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="f7e1a-129">Aby uzyskać więcej informacji na temat skalowania, zobacz [warstwy usług](../concepts-service-tiers.md) i [obliczeniowe i Magazyn jednostek](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f7e1a-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
