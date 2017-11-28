---
title: "aaaCreate i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate i zarządzanie bazą danych Azure dla PostgreSQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="10d86-103">Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="10d86-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="10d86-104">Reguły zapory poziomu serwera włączyć tooan dostępu toomanage administratorów bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="10d86-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="10d86-105">Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, można utworzyć, zaktualizować, Usuń, listy i Pokaż toomanage reguł zapory serwera.</span><span class="sxs-lookup"><span data-stu-id="10d86-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="10d86-106">Omówienie bazy danych Azure dla zapór PostgreSQL, zobacz [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="10d86-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10d86-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="10d86-107">Prerequisites</span></span>
<span data-ttu-id="10d86-108">toostep za pośrednictwem tego jak tooguide, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="10d86-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="10d86-109">[Bazy danych Azure PostgreSQL serwera i bazy danych](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="10d86-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="10d86-110">Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) wiersza polecenia narzędzia lub użyj hello powłoki chmury Azure w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="10d86-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="10d86-111">Konfigurowanie reguł zapory dla bazy danych platformy Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="10d86-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="10d86-112">Witaj [az postgres reguły zapory serwera-](/cli/azure/postgres/server/firewall-rule) reguły zapory tooconfigure używane są polecenia.</span><span class="sxs-lookup"><span data-stu-id="10d86-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="10d86-113">Lista reguł zapory</span><span class="sxs-lookup"><span data-stu-id="10d86-113">List firewall rules</span></span> 
<span data-ttu-id="10d86-114">toolist hello istniejących reguł zapory serwera na powitania serwera, uruchom hello [listy reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="10d86-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="10d86-115">dane wyjściowe Hello wymieniono hello reguły formatowania żadnego domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="10d86-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="10d86-116">Można użyć przełącznika hello `--output table` dla bardziej czytelnym formacie tabeli jako dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="10d86-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="10d86-117">Tworzenie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="10d86-117">Create firewall rule</span></span>
<span data-ttu-id="10d86-118">toocreate nowej reguły zapory na powitania serwera Uruchom hello [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="10d86-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="10d86-119">W tym przykładzie umożliwia zakres wszystkich serwera hello tooaccess adresy IP **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="10d86-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="10d86-120">Podaj tooallow pojedynczej tooaccess adres IP hello tego samego adresu, jak hello Start adresów IP i końcowemu adresowi IP, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="10d86-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="10d86-121">Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały utworzone, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="10d86-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="10d86-122">W przypadku awarii, hello zamiast output showserror tekst komunikatu.</span><span class="sxs-lookup"><span data-stu-id="10d86-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="10d86-123">Aktualizuj reguły zapory</span><span class="sxs-lookup"><span data-stu-id="10d86-123">Update firewall rule</span></span> 
<span data-ttu-id="10d86-124">Aktualizuj istniejącą regułę zapory na powitania serwera przy użyciu [aktualizacja reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="10d86-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="10d86-125">Podaj nazwę hello hello istniejącą regułę zapory jako dane wejściowe i hello start adresów IP i końcowy IP atrybutów tooupdate.</span><span class="sxs-lookup"><span data-stu-id="10d86-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="10d86-126">Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="10d86-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="10d86-127">W przypadku awarii, hello zamiast output showserror tekst komunikatu.</span><span class="sxs-lookup"><span data-stu-id="10d86-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="10d86-128">Jeśli nie istnieje reguła zapory hello, pobiera on utworzony za pomocą polecenia aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="10d86-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="10d86-129">Pokaż szczegóły reguły zapory</span><span class="sxs-lookup"><span data-stu-id="10d86-129">Show firewall rule details</span></span>
<span data-ttu-id="10d86-130">Szczegóły reguły dla serwera hello istniejących Zapora może także wyświetlać uruchamiając [Pokaż reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#show) polecenia.</span><span class="sxs-lookup"><span data-stu-id="10d86-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="10d86-131">Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, który został określony, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="10d86-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="10d86-132">W przypadku awarii, hello zamiast output showserror tekst komunikatu.</span><span class="sxs-lookup"><span data-stu-id="10d86-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="10d86-133">Usuwanie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="10d86-133">Delete firewall rule</span></span>
<span data-ttu-id="10d86-134">toorevoke dostępu dla zakresu adresów IP z serwera hello, usuń istniejącą regułę zapory, wykonując hello [az postgres reguły zapory serwera-Usuń](/cli/azure/postgres/server/firewall-rule#delete) polecenia.</span><span class="sxs-lookup"><span data-stu-id="10d86-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="10d86-135">Podaj nazwę hello hello istniejącej reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="10d86-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="10d86-136">Na sukces nie ma żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="10d86-136">Upon success, there is no output.</span></span> <span data-ttu-id="10d86-137">W przypadku awarii tekst komunikatu o błędzie hello jest zwracana.</span><span class="sxs-lookup"><span data-stu-id="10d86-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10d86-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10d86-138">Next steps</span></span>
- <span data-ttu-id="10d86-139">Podobnie za można używać przeglądarki sieci web[tworzenie i zarządzanie bazą danych Azure dla PostgreSQL reguł zapory przy użyciu hello portalu Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="10d86-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="10d86-140">Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="10d86-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="10d86-141">Aby uzyskać pomoc w łączenie tooan Azure bazy danych dla serwera PostgreSQL, [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="10d86-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
