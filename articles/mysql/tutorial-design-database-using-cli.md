---
title: "Projektowanie pierwszej bazy danych Azure, aby baza danych MySQL — wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym samouczku opisano sposób tworzenia i zarządzania nimi Azure bazy danych MySQL serwer i bazę danych, korzystając z wiersza polecenia Azure CLI 2.0."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="834b1-103">Projektowanie pierwszej bazy danych Azure, aby baza danych MySQL</span><span class="sxs-lookup"><span data-stu-id="834b1-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="834b1-104">Bazy danych platformy Azure dla programu MySQL jest usługą relacyjnych baz danych w chmurze firmy Microsoft, oparte na aparacie bazy danych MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="834b1-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="834b1-105">W tym samouczku używasz interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia Aby dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="834b1-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="834b1-106">Utwórz bazę danych systemu Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="834b1-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="834b1-107">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="834b1-107">Configure the server firewall</span></span>
> * <span data-ttu-id="834b1-108">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tworzenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="834b1-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="834b1-109">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="834b1-109">Load sample data</span></span>
> * <span data-ttu-id="834b1-110">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="834b1-110">Query data</span></span>
> * <span data-ttu-id="834b1-111">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="834b1-111">Update data</span></span>
> * <span data-ttu-id="834b1-112">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="834b1-112">Restore data</span></span>

<span data-ttu-id="834b1-113">Można użyć powłoki chmury Azure w przeglądarce lub [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli) na komputerze do uruchomienia bloki kodu w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="834b1-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="834b1-114">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="834b1-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="834b1-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="834b1-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="834b1-116">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="834b1-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="834b1-117">Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w której zasób istnieje lub dla której są za niego naliczane opłaty.</span><span class="sxs-lookup"><span data-stu-id="834b1-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="834b1-118">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="834b1-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="834b1-119">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="834b1-119">Create a resource group</span></span>
<span data-ttu-id="834b1-120">Utwórz [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) z [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="834b1-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="834b1-121">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="834b1-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="834b1-122">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `mycliresource` w lokalizacji `westus`.</span><span class="sxs-lookup"><span data-stu-id="834b1-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="834b1-123">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="834b1-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="834b1-124">Utwórz bazę danych Azure, MySQL serwera z serwerem mysql az Utwórz polecenie.</span><span class="sxs-lookup"><span data-stu-id="834b1-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="834b1-125">Serwer umożliwia zarządzanie wieloma bazami danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-125">A server can manage multiple databases.</span></span> <span data-ttu-id="834b1-126">Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="834b1-127">W poniższym przykładzie w regionie `westus` w grupie zasobów `mycliresource` jest tworzony serwer usługi Azure Database for MySQL o nazwie `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="834b1-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="834b1-128">Serwer ma identyfikator logowania administratora o nazwie `myadmin` i hasło `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="834b1-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="834b1-129">Serwer jest tworzony w ramach warstwy wydajności **Podstawowa** i z użyciem **50** jednostek obliczeniowych współdzielonych między wszystkimi bazami danych na tym serwerze.</span><span class="sxs-lookup"><span data-stu-id="834b1-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="834b1-130">Możesz skalować zasoby obliczeniowe i magazyn w górę lub w dół w zależności od potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="834b1-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="834b1-131">Konfigurowanie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="834b1-131">Configure firewall rule</span></span>
<span data-ttu-id="834b1-132">Utwórz bazę danych Azure, aby utworzyć regułę zapory poziomu serwera MySQL z az mysql reguły zapory serwera — polecenie.</span><span class="sxs-lookup"><span data-stu-id="834b1-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="834b1-133">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak **mysql** narzędzia wiersza polecenia lub MySQL Workbench, aby nawiązać połączenie z serwerem za pośrednictwem zapory usługi MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="834b1-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="834b1-134">Poniższy przykład powoduje utworzenie reguły zapory dla zakresu adresów wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="834b1-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="834b1-135">Ten przykład przedstawia całą możliwe zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="834b1-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="834b1-136">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="834b1-136">Get the connection information</span></span>

<span data-ttu-id="834b1-137">Aby nawiązać połączenie z serwerem, musisz podać informacje o hoście i poświadczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="834b1-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="834b1-138">Wynik jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="834b1-138">The result is in JSON format.</span></span> <span data-ttu-id="834b1-139">Zanotuj wartości **fullyQualifiedDomainName** i **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="834b1-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="834b1-140">Połącz z serwerem przy użyciu mysql</span><span class="sxs-lookup"><span data-stu-id="834b1-140">Connect to the server using mysql</span></span>
<span data-ttu-id="834b1-141">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) nawiązanie połączenia do bazy danych Azure, serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="834b1-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="834b1-142">W tym przykładzie to polecenie:</span><span class="sxs-lookup"><span data-stu-id="834b1-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="834b1-143">Tworzenie pustej bazy danych</span><span class="sxs-lookup"><span data-stu-id="834b1-143">Create a blank database</span></span>
<span data-ttu-id="834b1-144">Po nawiązaniu połączenia z serwerem, należy utworzyć pustą bazę danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="834b1-145">W wierszu polecenia Uruchom następujące polecenie, aby przełączyć połączenia do nowo utworzonej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="834b1-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="834b1-146">Tworzenie tabel w bazie danych</span><span class="sxs-lookup"><span data-stu-id="834b1-146">Create tables in the database</span></span>
<span data-ttu-id="834b1-147">Teraz, gdy wiesz, jak nawiązać połączenia z bazą danych Azure dla bazy danych MySQL, możemy przekazywane sposób wykonania zadania podstawowe.</span><span class="sxs-lookup"><span data-stu-id="834b1-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="834b1-148">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="834b1-149">Teraz utworzyć tabelę, która przechowuje informacje dotyczące spisu.</span><span class="sxs-lookup"><span data-stu-id="834b1-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="834b1-150">Ładowanie danych do tabel</span><span class="sxs-lookup"><span data-stu-id="834b1-150">Load data into the tables</span></span>
<span data-ttu-id="834b1-151">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="834b1-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="834b1-152">W oknie Otwórz okno wiersza polecenia Uruchom następujące zapytanie, aby wstawić niektórych wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="834b1-153">Masz teraz dwa wiersze przykładowych danych do tabeli utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="834b1-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="834b1-154">Zapytania i zaktualizować dane w tabelach</span><span class="sxs-lookup"><span data-stu-id="834b1-154">Query and update the data in the tables</span></span>
<span data-ttu-id="834b1-155">Wykonaj następujące zapytanie, aby pobrać informacje z tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="834b1-156">Należy również zaktualizować dane w tabelach.</span><span class="sxs-lookup"><span data-stu-id="834b1-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="834b1-157">Wiersz jest odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="834b1-158">Przywracanie bazy danych do określonego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="834b1-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="834b1-159">Załóżmy, że zostanie przypadkowo usunięte w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="834b1-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="834b1-160">Jest to coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="834b1-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="834b1-161">Bazy danych platformy Azure dla programu MySQL umożliwia wróć do dowolnego punktu w czasie w górę ostatnich 35 dni i przywrócić ten punkt w czasie na nowy serwer.</span><span class="sxs-lookup"><span data-stu-id="834b1-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="834b1-162">Możesz użyć tego nowego serwera, aby odzyskać usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="834b1-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="834b1-163">Poniższe kroki należy przywrócić działanie serwera próbki do punktu przed tabeli został dodany.</span><span class="sxs-lookup"><span data-stu-id="834b1-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="834b1-164">W przypadku przywracania należy następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="834b1-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="834b1-165">Punkt przywracania: Wybierz w momencie po serwer został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="834b1-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="834b1-166">Musi być większa niż lub równa wartości kopii zapasowej najstarsze źródłowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="834b1-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="834b1-167">Serwer docelowy: Podaj nową nazwę serwera mają zostać przywrócone</span><span class="sxs-lookup"><span data-stu-id="834b1-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="834b1-168">Serwer źródłowy: Podaj nazwę serwera, aby przywrócić z</span><span class="sxs-lookup"><span data-stu-id="834b1-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="834b1-169">Lokalizacja: Nie można wybrać region, domyślnie jest taki sam jak serwer źródłowy</span><span class="sxs-lookup"><span data-stu-id="834b1-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="834b1-170">Aby przywrócić serwer i [Przywracanie do punktu w czasie](./howto-restore-server-portal.md) przed tabeli został usunięty.</span><span class="sxs-lookup"><span data-stu-id="834b1-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="834b1-171">Przywracanie serwera do innego punktu w czasie tworzy zduplikowane nowy serwer jako oryginalnego serwera, począwszy od punktu w czasie, możesz określić, pod warunkiem, że w okresie przechowywania dla Twojego [warstwy usług](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="834b1-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="834b1-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="834b1-172">Next Steps</span></span>
<span data-ttu-id="834b1-173">W tym samouczku przedstawiono do:</span><span class="sxs-lookup"><span data-stu-id="834b1-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="834b1-174">Utwórz bazę danych systemu Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="834b1-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="834b1-175">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="834b1-175">Configure the server firewall</span></span>
> * <span data-ttu-id="834b1-176">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tworzenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="834b1-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="834b1-177">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="834b1-177">Load sample data</span></span>
> * <span data-ttu-id="834b1-178">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="834b1-178">Query data</span></span>
> * <span data-ttu-id="834b1-179">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="834b1-179">Update data</span></span>
> * <span data-ttu-id="834b1-180">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="834b1-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="834b1-181">Bazy danych platformy Azure dla programu MySQL — przykłady wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="834b1-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
