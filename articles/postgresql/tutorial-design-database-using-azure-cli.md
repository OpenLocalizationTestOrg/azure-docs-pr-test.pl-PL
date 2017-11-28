---
title: "Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak projektować pod kątem PostgreSQL pierwszą bazę danych Azure przy użyciu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="d851a-103">Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d851a-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="d851a-104">W tym samouczku używasz interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia Aby dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="d851a-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d851a-105">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d851a-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="d851a-106">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="d851a-106">Configure the server firewall</span></span>
> * <span data-ttu-id="d851a-107">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie do tworzenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="d851a-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="d851a-108">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="d851a-108">Load sample data</span></span>
> * <span data-ttu-id="d851a-109">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="d851a-109">Query data</span></span>
> * <span data-ttu-id="d851a-110">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="d851a-110">Update data</span></span>
> * <span data-ttu-id="d851a-111">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="d851a-111">Restore data</span></span>

<span data-ttu-id="d851a-112">Można użyć powłoki chmury Azure w przeglądarce lub [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli) na komputerze do uruchomienia bloki kodu w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d851a-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d851a-113">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d851a-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d851a-114">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="d851a-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="d851a-115">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d851a-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="d851a-116">Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w której zasób istnieje lub dla której są za niego naliczane opłaty.</span><span class="sxs-lookup"><span data-stu-id="d851a-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="d851a-117">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="d851a-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d851a-118">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d851a-118">Create a resource group</span></span>
<span data-ttu-id="d851a-119">Utwórz [grupę zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d851a-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d851a-120">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="d851a-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d851a-121">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myresourcegroup` w lokalizacji `westus`.</span><span class="sxs-lookup"><span data-stu-id="d851a-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="d851a-122">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d851a-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="d851a-123">Utwórz [serwer usługi Azure Database for PostgreSQL](overview.md) za pomocą polecenia [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="d851a-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="d851a-124">Serwer zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="d851a-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="d851a-125">Poniższy przykład tworzy serwer o nazwie `mypgserver-20170401` w grupie zasobów `myresourcegroup` z identyfikator logowania administratora serwera `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="d851a-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="d851a-126">Nazwa serwera mapuje nazwę DNS i w związku z tym musi być globalnie unikatowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d851a-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="d851a-127">Zastąp zmienną `<server_admin_password>` swoją własną wartością.</span><span class="sxs-lookup"><span data-stu-id="d851a-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="d851a-128">Login i hasło administratora serwera określone w tym miejscu będą wymagane do logowania do serwera i jego baz danych w późniejszej części tego przewodnika Szybki start.</span><span class="sxs-lookup"><span data-stu-id="d851a-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="d851a-129">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="d851a-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="d851a-130">Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze.</span><span class="sxs-lookup"><span data-stu-id="d851a-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="d851a-131">Baza danych [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) to domyślna baza danych przeznaczona do użycia dla użytkowników oraz na potrzeby narzędzi i aplikacji innych firm.</span><span class="sxs-lookup"><span data-stu-id="d851a-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="d851a-132">Konfigurowanie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="d851a-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="d851a-133">Utwórz regułę zapory na poziomie serwera Azure PostgreSQL za pomocą polecenia [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="d851a-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d851a-134">Reguła zapory na poziomie serwera pozwala aplikacji zewnętrznej, takiej jak narzędzie [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) lub [PgAdmin](https://www.pgadmin.org/), na nawiązywanie połączeń z Twoim serwerem przez zaporę usługi Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d851a-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="d851a-135">Możesz ustawić regułę zapory uwzględniającą zakres adresów IP, aby mieć możliwość nawiązywania połączeń z Twojej sieci.</span><span class="sxs-lookup"><span data-stu-id="d851a-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="d851a-136">W poniższym przykładzie użyto polecenia [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) w celu utworzenia reguły zapory `AllowAllIps` dla zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d851a-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="d851a-137">Aby otworzyć wszystkie adresy IP, użyj wartości 0.0.0.0 jako początkowego adresu IP i wartości 255.255.255.255 jako adresu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d851a-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="d851a-138">Serwer Azure PostgreSQL komunikuje się przez port 5432.</span><span class="sxs-lookup"><span data-stu-id="d851a-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="d851a-139">Podczas nawiązywania połączenia z sieci firmowej ruch wychodzący przez port 5432 może być blokowany przez zaporę sieciową.</span><span class="sxs-lookup"><span data-stu-id="d851a-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d851a-140">Aby było możliwe nawiązywanie połączenia z serwerem usługi Azure SQL Database, poproś dział IT o otwarcie portu 5432.</span><span class="sxs-lookup"><span data-stu-id="d851a-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="d851a-141">Uzyskiwanie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="d851a-141">Get the connection information</span></span>

<span data-ttu-id="d851a-142">Aby nawiązać połączenie z serwerem, musisz podać informacje o hoście i poświadczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="d851a-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="d851a-143">Wynik jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d851a-143">The result is in JSON format.</span></span> <span data-ttu-id="d851a-144">Zanotuj wartości **administratorLogin** i **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="d851a-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="d851a-145">Łączenia z bazą danych Azure PostgreSQL bazy danych przy użyciu psql</span><span class="sxs-lookup"><span data-stu-id="d851a-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="d851a-146">Jeśli komputer kliencki ma zainstalowany PostgreSQL, można użyć lokalnego wystąpienia programu [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), lub Azure Cloud Console do nawiązywania połączenia z serwerem Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d851a-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="d851a-147">Użyj teraz narzędzia wiersza polecenia psql, aby nawiązać połączenie z serwerem usługi Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d851a-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="d851a-148">Uruchom poniższe polecenie psql w celu nawiązania połączenia z serwerem usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d851a-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="d851a-149">Na przykład poniższe polecenie nawiązuje połączenie z domyślną bazą danych o nazwie **postgres** na Twoim serwerze PostgreSQL **mypgserver-20170401.postgres.database.azure.com** za pomocą poświadczeń dostępu.</span><span class="sxs-lookup"><span data-stu-id="d851a-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="d851a-150">Gdy zostanie wyświetlony monit o podanie hasła, wprowadź wybrane hasło `<server_admin_password>`.</span><span class="sxs-lookup"><span data-stu-id="d851a-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="d851a-151">Po nawiązaniu połączenia z serwerem utwórz pustą bazę danych za pomocą wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d851a-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="d851a-152">W wierszu polecenia wykonaj poniższe polecenie, aby przełączyć połączenie na nowo utworzoną bazę danych **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="d851a-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="d851a-153">Tworzenie tabel w bazie danych</span><span class="sxs-lookup"><span data-stu-id="d851a-153">Create tables in the database</span></span>
<span data-ttu-id="d851a-154">Teraz, Znając sposób nawiązywania połączenia z bazą danych Azure dla PostgreSQL możemy przekazywane sposób wykonania zadania podstawowe.</span><span class="sxs-lookup"><span data-stu-id="d851a-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="d851a-155">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="d851a-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="d851a-156">Ta funkcja pozwala utworzyć tabelę, która śledzi informacje o spisie.</span><span class="sxs-lookup"><span data-stu-id="d851a-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="d851a-157">Teraz wyświetlić nowo utworzona tabela listy tabel, wpisując:</span><span class="sxs-lookup"><span data-stu-id="d851a-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="d851a-158">Ładowanie danych do tabel</span><span class="sxs-lookup"><span data-stu-id="d851a-158">Load data into the tables</span></span>
<span data-ttu-id="d851a-159">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="d851a-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="d851a-160">W oknie Otwórz okno wiersza polecenia Uruchom następujące zapytanie do wstawienia niektórych wierszy danych</span><span class="sxs-lookup"><span data-stu-id="d851a-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="d851a-161">Masz teraz dwa wiersze przykładowych danych do tabeli utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d851a-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="d851a-162">Zapytania i zaktualizować dane w tabelach</span><span class="sxs-lookup"><span data-stu-id="d851a-162">Query and update the data in the tables</span></span>
<span data-ttu-id="d851a-163">Wykonaj następujące zapytanie, aby pobrać informacje z tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d851a-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="d851a-164">Możesz również zaktualizować dane w tabelach</span><span class="sxs-lookup"><span data-stu-id="d851a-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="d851a-165">Wiersz jest odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="d851a-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="d851a-166">Przywracanie bazy danych do określonego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="d851a-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="d851a-167">Załóżmy, że przypadkowo usunięto tabelę.</span><span class="sxs-lookup"><span data-stu-id="d851a-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="d851a-168">Jest to coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="d851a-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="d851a-169">Bazy danych platformy Azure dla PostgreSQL umożliwia wróć do dowolnego punktu na czas (w ostatnim maksymalnie 7 dni (Basic), a 35 dni (standardowe)) i przywrócić tego punktu w czasie na nowy serwer.</span><span class="sxs-lookup"><span data-stu-id="d851a-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="d851a-170">Możesz użyć tego nowego serwera, aby odzyskać usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="d851a-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="d851a-171">Poniższe kroki należy przywrócić działanie serwera próbki do punktu przed tabeli został dodany.</span><span class="sxs-lookup"><span data-stu-id="d851a-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="d851a-172">`az postgres server restore` Polecenia wymaga następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="d851a-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="d851a-173">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="d851a-173">Setting</span></span> | <span data-ttu-id="d851a-174">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="d851a-174">Suggested value</span></span> | <span data-ttu-id="d851a-175">Opis</span><span class="sxs-lookup"><span data-stu-id="d851a-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="d851a-176">--grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d851a-176">--resource-group</span></span> |  <span data-ttu-id="d851a-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d851a-177">myResourceGroup</span></span> |  <span data-ttu-id="d851a-178">Grupy zasobów, w której serwer źródłowy istnieje.</span><span class="sxs-lookup"><span data-stu-id="d851a-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="d851a-179">— Nazwa</span><span class="sxs-lookup"><span data-stu-id="d851a-179">--name</span></span> | <span data-ttu-id="d851a-180">przywrócona mypgserver</span><span class="sxs-lookup"><span data-stu-id="d851a-180">mypgserver-restored</span></span> | <span data-ttu-id="d851a-181">Nazwa nowego serwera, który jest tworzony przez polecenie restore.</span><span class="sxs-lookup"><span data-stu-id="d851a-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="d851a-182">Przywracanie punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="d851a-182">restore-point-in-time</span></span> | <span data-ttu-id="d851a-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="d851a-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="d851a-184">Wybierz w momencie przywrócić.</span><span class="sxs-lookup"><span data-stu-id="d851a-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="d851a-185">Ta data i godzina musi być w okresie przechowywania kopii zapasowej serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="d851a-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="d851a-186">Użyj formatu ISO8601 daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="d851a-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="d851a-187">Na przykład możesz może używać własnych lokalnej strefie czasowej, takich jak `2017-04-13T05:59:00-08:00`, lub użyj formatu czasu UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="d851a-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="d851a-188">--serwera źródłowego</span><span class="sxs-lookup"><span data-stu-id="d851a-188">--source-server</span></span> | <span data-ttu-id="d851a-189">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="d851a-189">mypgserver-20170401</span></span> | <span data-ttu-id="d851a-190">Nazwa lub identyfikator serwera źródłowego, aby przywrócić z.</span><span class="sxs-lookup"><span data-stu-id="d851a-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="d851a-191">Przywracanie do punktu w czasie serwer tworzy nowy serwer, kopiowanie jako oryginalnego serwera, począwszy od punktu w czasie, które określisz.</span><span class="sxs-lookup"><span data-stu-id="d851a-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="d851a-192">Lokalizacja i wartości warstwy cenowej przywróconej serwera są takie same, jak na serwerze źródłowym.</span><span class="sxs-lookup"><span data-stu-id="d851a-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="d851a-193">Polecenie jest synchroniczne i zwróci po przywróceniu serwera.</span><span class="sxs-lookup"><span data-stu-id="d851a-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="d851a-194">Po zakończeniu przywracania, zlokalizuj nowy serwer, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="d851a-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="d851a-195">Sprawdź, czy dane została przywrócona, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="d851a-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d851a-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d851a-196">Next steps</span></span>
<span data-ttu-id="d851a-197">W tym samouczku przedstawiono sposób użycia interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia do:</span><span class="sxs-lookup"><span data-stu-id="d851a-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d851a-198">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d851a-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="d851a-199">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="d851a-199">Configure the server firewall</span></span>
> * <span data-ttu-id="d851a-200">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie do tworzenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="d851a-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="d851a-201">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="d851a-201">Load sample data</span></span>
> * <span data-ttu-id="d851a-202">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="d851a-202">Query data</span></span>
> * <span data-ttu-id="d851a-203">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="d851a-203">Update data</span></span>
> * <span data-ttu-id="d851a-204">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="d851a-204">Restore data</span></span>

<span data-ttu-id="d851a-205">Następnie Dowiedz się, jak używać portalu Azure do wykonywania zadań podobne, zapoznaj się w tym samouczku: [projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu portalu Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d851a-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
