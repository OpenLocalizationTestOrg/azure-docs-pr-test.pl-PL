---
title: "Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia i zarządzania bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="795a5-103">Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="795a5-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="795a5-104">Reguły zapory poziomu serwera umożliwiają administratorom zarządzanie dostępem do bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="795a5-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="795a5-105">Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, możesz utworzyć, zaktualizować, Usuń listę i Pokaż reguły zapory do zarządzania serwerem.</span><span class="sxs-lookup"><span data-stu-id="795a5-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="795a5-106">Omówienie bazy danych Azure dla zapór PostgreSQL, zobacz [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="795a5-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="795a5-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="795a5-107">Prerequisites</span></span>
<span data-ttu-id="795a5-108">Do wykonania kroków opisanych ten przewodnik, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="795a5-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="795a5-109">[Bazy danych Azure PostgreSQL serwera i bazy danych](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="795a5-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="795a5-110">Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) narzędzia wiersza polecenia lub użyć powłoki chmury Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="795a5-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="795a5-111">Konfigurowanie reguł zapory dla bazy danych platformy Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="795a5-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="795a5-112">[Az postgres reguły zapory serwera-](/cli/azure/postgres/server/firewall-rule) polecenia są używane do konfigurowania reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="795a5-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="795a5-113">Lista reguł zapory</span><span class="sxs-lookup"><span data-stu-id="795a5-113">List firewall rules</span></span> 
<span data-ttu-id="795a5-114">Aby wyświetlić listę istniejących reguł zapory serwera na serwerze, uruchom [listy reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="795a5-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="795a5-115">Dane wyjściowe wymieniono reguły, jeśli istnieje domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="795a5-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="795a5-116">Można użyć przełącznika `--output table` dla bardziej czytelnym formacie tabeli jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="795a5-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="795a5-117">Tworzenie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="795a5-117">Create firewall rule</span></span>
<span data-ttu-id="795a5-118">Aby utworzyć nową regułę zapory na serwerze, uruchom [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="795a5-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="795a5-119">W tym przykładzie umożliwia zakres wszystkie adresy IP na dostęp do serwera **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="795a5-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="795a5-120">Aby umożliwić pojedynczej adresu IP uzyskać dostęp, podaj ten sam adres Start IP i End IP, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="795a5-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="795a5-121">Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały utworzone, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="795a5-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="795a5-122">Jeśli występuje awaria, tekst komunikatu showserror danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="795a5-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="795a5-123">Aktualizuj reguły zapory</span><span class="sxs-lookup"><span data-stu-id="795a5-123">Update firewall rule</span></span> 
<span data-ttu-id="795a5-124">Aktualizuj istniejącą regułę zapory na serwerze przy użyciu [aktualizacja reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="795a5-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="795a5-125">Podaj nazwę istniejącej reguły zapory jako dane wejściowe i uruchom atrybutów IP adresów IP i końcowy do aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="795a5-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="795a5-126">Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="795a5-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="795a5-127">Jeśli występuje awaria, tekst komunikatu showserror danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="795a5-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="795a5-128">Jeśli reguły zapory nie istnieje, pobiera on utworzony za pomocą polecenia aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="795a5-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="795a5-129">Pokaż szczegóły reguły zapory</span><span class="sxs-lookup"><span data-stu-id="795a5-129">Show firewall rule details</span></span>
<span data-ttu-id="795a5-130">Szczegóły reguły dla serwera istniejących Zapora może także wyświetlać uruchamiając [Pokaż reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#show) polecenia.</span><span class="sxs-lookup"><span data-stu-id="795a5-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="795a5-131">Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, który został określony, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="795a5-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="795a5-132">Jeśli występuje awaria, tekst komunikatu showserror danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="795a5-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="795a5-133">Usuwanie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="795a5-133">Delete firewall rule</span></span>
<span data-ttu-id="795a5-134">Aby odwołać dostępu dla zakresu adresów IP z serwera, usuń istniejącą regułę zapory, wykonując [az postgres reguły zapory serwera-Usuń](/cli/azure/postgres/server/firewall-rule#delete) polecenia.</span><span class="sxs-lookup"><span data-stu-id="795a5-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="795a5-135">Podaj nazwę istniejącej reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="795a5-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="795a5-136">Na sukces nie ma żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="795a5-136">Upon success, there is no output.</span></span> <span data-ttu-id="795a5-137">W przypadku awarii zwracana jest tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="795a5-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="795a5-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="795a5-138">Next steps</span></span>
- <span data-ttu-id="795a5-139">Analogicznie, można użyć przeglądarki sieci web [tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu portalu Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="795a5-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="795a5-140">Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="795a5-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="795a5-141">Aby uzyskać pomoc w połączeniu z bazą danych PostgreSQL serwera Azure, zobacz [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="795a5-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
