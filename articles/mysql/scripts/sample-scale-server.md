---
title: "Przykładów dla interfejsu wiersza polecenia platformy Azure można skalować bazy danych Azure dla serwera MySQL | Dokumentacja firmy Microsoft"
description: "Ten przykładowy skrypt interfejsu wiersza polecenia skaluje Azure bazy danych MySQL serwera do poziomu wydajności różnych po zapytań metryki."
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
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="4665e-103">Monitorowanie i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4665e-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="4665e-104">Ten przykładowy skrypt CLI skaluje pojedynczej bazy danych Azure MySQL serwera do poziomu wydajności różnych po zapytań metryki.</span><span class="sxs-lookup"><span data-stu-id="4665e-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4665e-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4665e-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4665e-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="4665e-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="4665e-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4665e-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4665e-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="4665e-108">Sample script</span></span>
<span data-ttu-id="4665e-109">Ten przykładowy skrypt Zmień wyróżnione wiersze w celu dostosowania nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="4665e-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="4665e-110">Zastąp identyfikator subskrypcji używane w poleceniach monitor az z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4665e-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="4665e-111">[!code-azurecli-interactive[główne](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "tworzenia i skalowania bazy danych Azure dla programu MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="4665e-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4665e-112">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4665e-112">Clean up deployment</span></span>
<span data-ttu-id="4665e-113">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="4665e-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="4665e-114">[!code-azurecli-interactive[główne](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Usuń grupę zasobów.")]</span><span class="sxs-lookup"><span data-stu-id="4665e-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="4665e-115">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="4665e-115">Script explanation</span></span>
<span data-ttu-id="4665e-116">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="4665e-116">This script uses the following commands.</span></span> <span data-ttu-id="4665e-117">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4665e-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4665e-118">**Polecenie**</span><span class="sxs-lookup"><span data-stu-id="4665e-118">**Command**</span></span> | <span data-ttu-id="4665e-119">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="4665e-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="4665e-120">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="4665e-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4665e-121">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="4665e-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4665e-122">utworzenie przez serwer mysql az</span><span class="sxs-lookup"><span data-stu-id="4665e-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="4665e-123">Tworzy serwer MySQL, który jest hostem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4665e-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="4665e-124">Lista metryki monitor az</span><span class="sxs-lookup"><span data-stu-id="4665e-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="4665e-125">Wyświetl listę wartość metryki dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="4665e-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="4665e-126">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="4665e-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="4665e-127">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="4665e-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4665e-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4665e-128">Next steps</span></span>
- <span data-ttu-id="4665e-129">Przeczytaj więcej informacji na temat interfejsu wiersza polecenia Azure: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4665e-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="4665e-130">Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="4665e-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="4665e-131">Aby uzyskać więcej informacji na temat skalowania, zobacz [warstwy usług](../concepts-service-tiers.md) i [obliczeniowe i Magazyn jednostek](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4665e-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
