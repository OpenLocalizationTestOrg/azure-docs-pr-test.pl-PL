---
title: "AAA \"Azure CLI skryptu — tworzenie bazy danych platformy Azure dla programu MySQL | Dokumentacja firmy Microsoft\""
description: "Ten przykładowy skrypt interfejsu wiersza polecenia Azure bazy danych serwera MySQL tworzy i konfiguruje regułę zapory poziomu serwera."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="80c92-103">Utwórz serwer MySQL i skonfigurować regułę zapory przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="80c92-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="80c92-104">Ten przykładowy skrypt interfejsu wiersza polecenia Azure bazy danych serwera MySQL tworzy i konfiguruje regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="80c92-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="80c92-105">Po pomyślnym uruchomieniu skryptu hello hello MySQL serwer jest dostępny dla wszystkich usług platformy Azure i hello skonfigurowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="80c92-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="80c92-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="80c92-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="80c92-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="80c92-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="80c92-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="80c92-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="80c92-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="80c92-109">Sample script</span></span>
<span data-ttu-id="80c92-110">W ten przykładowy skrypt edytować hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="80c92-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="80c92-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="80c92-111">Clean up deployment</span></span>
<span data-ttu-id="80c92-112">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="80c92-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="80c92-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="80c92-113">Script explanation</span></span>
<span data-ttu-id="80c92-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="80c92-114">This script uses hello following commands.</span></span> <span data-ttu-id="80c92-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="80c92-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="80c92-116">**Polecenie**</span><span class="sxs-lookup"><span data-stu-id="80c92-116">**Command**</span></span> | <span data-ttu-id="80c92-117">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="80c92-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="80c92-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="80c92-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="80c92-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="80c92-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="80c92-120">utworzenie przez serwer mysql az</span><span class="sxs-lookup"><span data-stu-id="80c92-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="80c92-121">Tworzy serwer MySQL obsługującego hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="80c92-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="80c92-122">Utwórz az mysql Serwer zapory</span><span class="sxs-lookup"><span data-stu-id="80c92-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="80c92-123">Tworzy serwer toohello dostępu tooallow reguły zapory i baz danych z zakresu adresów IP hello wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="80c92-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="80c92-124">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="80c92-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="80c92-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="80c92-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80c92-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80c92-126">Next steps</span></span>
- <span data-ttu-id="80c92-127">Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80c92-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="80c92-128">Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="80c92-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
