---
title: AAA "Azure CLI Script - tworzenie bazy danych platformy Azure dla PostgreSQL | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie — tworzy Azure bazy danych serwera PostgreSQL i konfiguruje regułę zapory poziomu serwera."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="3222d-103">Utwórz bazę danych Azure dla serwera PostgreSQL i skonfigurować regułę zapory przy użyciu interfejsu wiersza polecenia Azure hello</span><span class="sxs-lookup"><span data-stu-id="3222d-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="3222d-104">Ten przykładowy skrypt interfejsu wiersza polecenia Azure bazy danych serwera PostgreSQL tworzy i konfiguruje regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="3222d-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="3222d-105">Po pomyślnym uruchomieniu skryptu powitania serwera PostgreSQL hello miała dostęp do wszystkich usług platformy Azure i hello skonfigurowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="3222d-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3222d-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3222d-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3222d-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="3222d-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3222d-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3222d-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3222d-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="3222d-109">Sample script</span></span>
<span data-ttu-id="3222d-110">W ten przykładowy skrypt edytować hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="3222d-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3222d-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3222d-111">Clean up deployment</span></span>
<span data-ttu-id="3222d-112">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="3222d-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="3222d-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="3222d-113">Script explanation</span></span>
<span data-ttu-id="3222d-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="3222d-114">This script uses hello following commands.</span></span> <span data-ttu-id="3222d-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="3222d-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3222d-116">**Polecenie**</span><span class="sxs-lookup"><span data-stu-id="3222d-116">**Command**</span></span> | <span data-ttu-id="3222d-117">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="3222d-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="3222d-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="3222d-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="3222d-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="3222d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3222d-120">utworzenie przez serwer postgres az</span><span class="sxs-lookup"><span data-stu-id="3222d-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="3222d-121">Tworzy serwer PostgreSQL obsługującego hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="3222d-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="3222d-122">Utwórz az postgres Serwer zapory</span><span class="sxs-lookup"><span data-stu-id="3222d-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="3222d-123">Tworzy serwer toohello dostępu tooallow reguły zapory i baz danych z zakresu adresów IP hello wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="3222d-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="3222d-124">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="3222d-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="3222d-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="3222d-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3222d-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3222d-126">Next steps</span></span>
- <span data-ttu-id="3222d-127">Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="3222d-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="3222d-128">Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3222d-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
