---
title: "Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak tooDesign Twojego pierwszego Azure bazy danych PostgreSQL przy użyciu wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="38e54-103">Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38e54-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="38e54-104">W tym samouczku używasz interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="38e54-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="38e54-105">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="38e54-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="38e54-106">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="38e54-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="38e54-107">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate Narzędzia bazy danych</span><span class="sxs-lookup"><span data-stu-id="38e54-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="38e54-108">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="38e54-108">Load sample data</span></span>
> * <span data-ttu-id="38e54-109">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="38e54-109">Query data</span></span>
> * <span data-ttu-id="38e54-110">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="38e54-110">Update data</span></span>
> * <span data-ttu-id="38e54-111">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="38e54-111">Restore data</span></span>

<span data-ttu-id="38e54-112">Możesz użyć hello powłoki chmury Azure w przeglądarce hello lub [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli) na własne bloki kodu komputera toorun hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="38e54-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="38e54-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="38e54-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="38e54-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="38e54-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="38e54-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38e54-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="38e54-116">Jeśli masz wiele subskrypcji, wybierz hello odpowiednie subskrypcji, w którym hello zasobów istnieje lub jest on rozliczany dla.</span><span class="sxs-lookup"><span data-stu-id="38e54-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="38e54-117">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="38e54-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="38e54-118">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="38e54-118">Create a resource group</span></span>
<span data-ttu-id="38e54-119">Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38e54-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="38e54-120">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="38e54-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="38e54-121">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myresourcegroup` w hello `westus` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="38e54-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="38e54-122">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="38e54-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="38e54-123">Utwórz [Azure bazy danych serwera PostgreSQL](overview.md) przy użyciu hello [utworzenie przez serwer postgres az](/cli/azure/postgres/server#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38e54-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="38e54-124">Serwer zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="38e54-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="38e54-125">Witaj poniższy przykład tworzy serwer o nazwie `mypgserver-20170401` w grupie zasobów `myresourcegroup` z identyfikator logowania administratora serwera `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="38e54-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="38e54-126">Nazwa serwera mapuje nazwę tooDNS i w związku z tym jest wymagana toobe globalnie unikatowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="38e54-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="38e54-127">SUBSTITUTE hello `<server_admin_password>` o własne wartości.</span><span class="sxs-lookup"><span data-stu-id="38e54-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="38e54-128">Hello identyfikator logowania administratora serwera i hasło, które są określone w tym miejscu są wymagane toolog Server toohello i jej baz danych w dalszej części tego szybki start.</span><span class="sxs-lookup"><span data-stu-id="38e54-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="38e54-129">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="38e54-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="38e54-130">Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze.</span><span class="sxs-lookup"><span data-stu-id="38e54-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="38e54-131">Witaj [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) baza danych jest domyślna baza danych przeznaczone do użytku przez użytkowników, narzędzia i aplikacje innych producentów.</span><span class="sxs-lookup"><span data-stu-id="38e54-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="38e54-132">Konfigurowanie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="38e54-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="38e54-133">Utwórz regułę zapory poziomu serwera Azure PostgreSQL z hello [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38e54-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="38e54-134">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) lub [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="38e54-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="38e54-135">Można ustawić reguły zapory, która obejmuje IP zakresu toobe stanie tooconnect z sieci.</span><span class="sxs-lookup"><span data-stu-id="38e54-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="38e54-136">Witaj poniższym przykładzie użyto [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) toocreate regułę zapory `AllowAllIps` zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="38e54-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="38e54-137">tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.</span><span class="sxs-lookup"><span data-stu-id="38e54-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="38e54-138">Serwer Azure PostgreSQL komunikuje się przez port 5432.</span><span class="sxs-lookup"><span data-stu-id="38e54-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="38e54-139">Podczas nawiązywania połączenia z sieci firmowej ruch wychodzący przez port 5432 może być blokowany przez zaporę sieciową.</span><span class="sxs-lookup"><span data-stu-id="38e54-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="38e54-140">Ma dział IT, otwórz port 5432 tooconnect tooyour bazy danych SQL Azure serwera.</span><span class="sxs-lookup"><span data-stu-id="38e54-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="38e54-141">Pobierz informacje o połączeniu hello</span><span class="sxs-lookup"><span data-stu-id="38e54-141">Get hello connection information</span></span>

<span data-ttu-id="38e54-142">tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="38e54-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="38e54-143">wynik Hello jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="38e54-143">hello result is in JSON format.</span></span> <span data-ttu-id="38e54-144">Zanotuj hello **administratorLogin** i **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="38e54-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="38e54-145">Połącz tooAzure bazy danych dla bazy danych PostgreSQL przy użyciu psql</span><span class="sxs-lookup"><span data-stu-id="38e54-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="38e54-146">Jeśli komputer kliencki ma zainstalowany PostgreSQL, można użyć lokalnego wystąpienia programu [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), lub hello Azure Cloud Console tooconnect tooan Azure PostgreSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="38e54-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="38e54-147">Użyjmy teraz hello psql narzędzia wiersza polecenia tooconnect toohello bazy danych Azure, PostgreSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="38e54-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="38e54-148">Uruchom następujące polecenie psql tooconnect tooan Azure bazy danych dla serwera PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="38e54-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="38e54-149">Na przykład następujące polecenie hello łączy toohello domyślna baza danych o nazwie **postgres** na serwerze PostgreSQL **mypgserver 20170401.postgres.database.azure.com** przy użyciu poświadczeń dostępu.</span><span class="sxs-lookup"><span data-stu-id="38e54-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="38e54-150">Wprowadź hello `<server_admin_password>` wybrano po wyświetleniu monitu o hasło.</span><span class="sxs-lookup"><span data-stu-id="38e54-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="38e54-151">Po przejściu toohello podłączonego serwera, należy utworzyć pustą bazę danych, w wierszu hello.</span><span class="sxs-lookup"><span data-stu-id="38e54-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="38e54-152">W wierszu polecenia hello wykonania hello następujące polecenia tooswitch połączenia toohello nowo utworzone w bazie danych **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="38e54-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="38e54-153">Tworzenie tabel w bazie danych hello</span><span class="sxs-lookup"><span data-stu-id="38e54-153">Create tables in hello database</span></span>
<span data-ttu-id="38e54-154">Teraz, gdy wiesz, jak toohello tooconnect bazą danych Azure dla PostgreSQL, firma Microsoft może przejść w sposób toocomplete niektóre podstawowe zadania.</span><span class="sxs-lookup"><span data-stu-id="38e54-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="38e54-155">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="38e54-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="38e54-156">Ta funkcja pozwala utworzyć tabelę, która śledzi informacje o spisie.</span><span class="sxs-lookup"><span data-stu-id="38e54-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="38e54-157">Można wyświetlić hello nowo utworzony tabeli w hello listy tabel teraz, wpisując:</span><span class="sxs-lookup"><span data-stu-id="38e54-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="38e54-158">Ładowanie danych do tabel hello</span><span class="sxs-lookup"><span data-stu-id="38e54-158">Load data into hello tables</span></span>
<span data-ttu-id="38e54-159">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="38e54-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="38e54-160">W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych</span><span class="sxs-lookup"><span data-stu-id="38e54-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="38e54-161">Masz teraz dwa wiersze przykładowych danych do tabeli hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="38e54-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="38e54-162">Zapytania i Aktualizuj hello dane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="38e54-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="38e54-163">Wykonanie poniższych informacji tooretrieve zapytania z tabeli bazy danych hello hello.</span><span class="sxs-lookup"><span data-stu-id="38e54-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="38e54-164">Można także zaktualizować hello dane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="38e54-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="38e54-165">wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="38e54-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="38e54-166">Przywracanie bazy danych tooa poprzedniego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="38e54-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="38e54-167">Załóżmy, że przypadkowo usunięto tabelę.</span><span class="sxs-lookup"><span data-stu-id="38e54-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="38e54-168">Jest to coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="38e54-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="38e54-169">Bazy danych platformy Azure dla PostgreSQL umożliwia toogo tooany Wstecz w momencie (w hello ostatnich dni too7 (Basic) i 35 dni (standardowe)) i przywracania w momencie tooa nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="38e54-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="38e54-170">Można użyć tego nowego serwera toorecover usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="38e54-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="38e54-171">Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="38e54-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="38e54-172">Witaj `az postgres server restore` polecenie musi hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="38e54-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="38e54-173">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="38e54-173">Setting</span></span> | <span data-ttu-id="38e54-174">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="38e54-174">Suggested value</span></span> | <span data-ttu-id="38e54-175">Opis</span><span class="sxs-lookup"><span data-stu-id="38e54-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="38e54-176">--grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="38e54-176">--resource-group</span></span> |  <span data-ttu-id="38e54-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38e54-177">myResourceGroup</span></span> |  <span data-ttu-id="38e54-178">Grupy zasobów, w których hello istnieje serwer źródłowy.</span><span class="sxs-lookup"><span data-stu-id="38e54-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="38e54-179">— Nazwa</span><span class="sxs-lookup"><span data-stu-id="38e54-179">--name</span></span> | <span data-ttu-id="38e54-180">przywrócona mypgserver</span><span class="sxs-lookup"><span data-stu-id="38e54-180">mypgserver-restored</span></span> | <span data-ttu-id="38e54-181">Nazwa Hello hello nowy serwer, który jest tworzony przez polecenie restore hello.</span><span class="sxs-lookup"><span data-stu-id="38e54-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="38e54-182">Przywracanie punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="38e54-182">restore-point-in-time</span></span> | <span data-ttu-id="38e54-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="38e54-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="38e54-184">Wybierz toorestore punktu w czasie, aby.</span><span class="sxs-lookup"><span data-stu-id="38e54-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="38e54-185">Ta data i godzina musi być w okresie przechowywania kopii zapasowej serwera źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="38e54-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="38e54-186">Użyj formatu ISO8601 daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="38e54-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="38e54-187">Na przykład możesz może używać własnych lokalnej strefie czasowej, takich jak `2017-04-13T05:59:00-08:00`, lub użyj formatu czasu UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="38e54-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="38e54-188">--serwera źródłowego</span><span class="sxs-lookup"><span data-stu-id="38e54-188">--source-server</span></span> | <span data-ttu-id="38e54-189">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="38e54-189">mypgserver-20170401</span></span> | <span data-ttu-id="38e54-190">Witaj, nazwa lub identyfikator toorestore serwera źródłowego hello z.</span><span class="sxs-lookup"><span data-stu-id="38e54-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="38e54-191">Przywracanie serwera tooa w momencie tworzy nowy serwer, kopiowanie jako hello oryginalnego serwera na powitania punktu w czasie, które określisz.</span><span class="sxs-lookup"><span data-stu-id="38e54-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="38e54-192">Hello lokalizacji i cenach wartości warstwy hello przywróceniu serwera są hello taki sam jak powitania serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="38e54-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="38e54-193">polecenie Hello jest synchroniczne i zwróci po przywróceniu powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="38e54-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="38e54-194">Po zakończeniu przywracania hello zlokalizować hello nowy serwer, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="38e54-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="38e54-195">Sprawdź hello danych zostało przywrócone, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="38e54-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="38e54-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38e54-196">Next steps</span></span>
<span data-ttu-id="38e54-197">W tym samouczku można przedstawiono sposób toouse wiersza polecenia platformy Azure (interfejsu wiersza polecenia) i inne narzędzia do:</span><span class="sxs-lookup"><span data-stu-id="38e54-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="38e54-198">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="38e54-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="38e54-199">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="38e54-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="38e54-200">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate Narzędzia bazy danych</span><span class="sxs-lookup"><span data-stu-id="38e54-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="38e54-201">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="38e54-201">Load sample data</span></span>
> * <span data-ttu-id="38e54-202">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="38e54-202">Query data</span></span>
> * <span data-ttu-id="38e54-203">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="38e54-203">Update data</span></span>
> * <span data-ttu-id="38e54-204">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="38e54-204">Restore data</span></span>

<span data-ttu-id="38e54-205">Następnie Dowiedz się, jak toouse hello podobne zadania toodo portalu Azure, przejrzyj tego samouczka: [projektowania pierwszą bazę danych Azure za pomocą PostgreSQL hello portalu Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="38e54-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
