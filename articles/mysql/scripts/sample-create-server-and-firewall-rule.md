---
title: "Azure CLI skryptu — tworzenie bazy danych platformy Azure dla programu MySQL | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 201db294ce362ef3e09cbe62f48bd51c8ea94dbb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="f213e-103">Utwórz serwer MySQL i skonfigurować regułę zapory przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f213e-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="f213e-104">Ten przykładowy skrypt interfejsu wiersza polecenia Azure bazy danych serwera MySQL tworzy i konfiguruje regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="f213e-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="f213e-105">Po pomyślnym uruchomieniu skryptu serwer MySQL jest dostępny dla wszystkich usług platformy Azure i skonfigurowanego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="f213e-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f213e-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f213e-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f213e-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="f213e-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="f213e-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f213e-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f213e-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f213e-109">Sample script</span></span>
<span data-ttu-id="f213e-110">W ten przykładowy skrypt edytować wyróżnione wiersze w celu dostosowania nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f213e-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="f213e-111">[!code-azurecli-interactive[główne](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "utworzenia bazy danych Azure MySQL i reguły zapory poziomu serwera.")]</span><span class="sxs-lookup"><span data-stu-id="f213e-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f213e-112">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f213e-112">Clean up deployment</span></span>
<span data-ttu-id="f213e-113">Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="f213e-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="f213e-114">[!code-azurecli-interactive[główne](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Usuń grupę zasobów.")]</span><span class="sxs-lookup"><span data-stu-id="f213e-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="f213e-115">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f213e-115">Script explanation</span></span>
<span data-ttu-id="f213e-116">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="f213e-116">This script uses the following commands.</span></span> <span data-ttu-id="f213e-117">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f213e-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f213e-118">**Polecenie**</span><span class="sxs-lookup"><span data-stu-id="f213e-118">**Command**</span></span> | <span data-ttu-id="f213e-119">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="f213e-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="f213e-120">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f213e-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="f213e-121">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f213e-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f213e-122">utworzenie przez serwer mysql az</span><span class="sxs-lookup"><span data-stu-id="f213e-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="f213e-123">Tworzy serwer MySQL, który jest hostem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f213e-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="f213e-124">Utwórz az mysql Serwer zapory</span><span class="sxs-lookup"><span data-stu-id="f213e-124">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="f213e-125">Tworzy regułę zapory, aby zezwolić na dostęp do serwera i baz danych z wprowadzony zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="f213e-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="f213e-126">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="f213e-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="f213e-127">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f213e-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f213e-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f213e-128">Next steps</span></span>
- <span data-ttu-id="f213e-129">Przeczytaj więcej informacji na temat interfejsu wiersza polecenia Azure: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f213e-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="f213e-130">Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f213e-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
