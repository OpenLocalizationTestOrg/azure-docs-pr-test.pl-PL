---
title: "aaaDesign pierwszy Azure bazy danych dla bazy danych MySQL — wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek wyjaśnia sposób toocreate i zarządzanie bazą danych Azure MySQL serwera i bazy danych przy użyciu usługi Azure CLI 2.0 z wiersza polecenia hello."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="b48b6-103">Projektowanie pierwszej bazy danych Azure, aby baza danych MySQL</span><span class="sxs-lookup"><span data-stu-id="b48b6-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="b48b6-104">Bazy danych platformy Azure dla programu MySQL jest usługą relacyjnych baz danych w hello firmy Microsoft w chmurze oparte na aparacie bazy danych MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="b48b6-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="b48b6-105">W tym samouczku używasz interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="b48b6-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b48b6-106">Utwórz bazę danych systemu Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="b48b6-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="b48b6-107">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="b48b6-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="b48b6-108">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bazy danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="b48b6-109">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="b48b6-109">Load sample data</span></span>
> * <span data-ttu-id="b48b6-110">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="b48b6-110">Query data</span></span>
> * <span data-ttu-id="b48b6-111">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-111">Update data</span></span>
> * <span data-ttu-id="b48b6-112">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-112">Restore data</span></span>

<span data-ttu-id="b48b6-113">Możesz użyć hello powłoki chmury Azure w przeglądarce hello lub [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli) na własne bloki kodu komputera toorun hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b48b6-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b48b6-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b48b6-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b48b6-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="b48b6-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b48b6-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b48b6-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="b48b6-117">Jeśli masz wiele subskrypcji, wybierz hello odpowiednie subskrypcji, w którym hello zasobów istnieje lub jest on rozliczany dla.</span><span class="sxs-lookup"><span data-stu-id="b48b6-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="b48b6-118">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="b48b6-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="b48b6-119">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="b48b6-119">Create a resource group</span></span>
<span data-ttu-id="b48b6-120">Utwórz [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) z [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b48b6-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="b48b6-121">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="b48b6-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="b48b6-122">Witaj poniższy przykład tworzy grupę zasobów o nazwie `mycliresource` w hello `westus` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b48b6-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="b48b6-123">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="b48b6-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="b48b6-124">Utwórz bazę danych Azure, dla polecenia Utwórz MySQL co serwer hello az mysql.</span><span class="sxs-lookup"><span data-stu-id="b48b6-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="b48b6-125">Serwer umożliwia zarządzanie wieloma bazami danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-125">A server can manage multiple databases.</span></span> <span data-ttu-id="b48b6-126">Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="b48b6-127">Witaj poniższy przykład tworzy Azure bazę danych MySQL serwera znajduje się w `westus` w grupie zasobów hello `mycliresource` o nazwie `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="b48b6-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="b48b6-128">powitania serwera zawiera dziennik administratora w nazwie `myadmin` i hasło `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="b48b6-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="b48b6-129">Serwer Hello jest tworzony z **podstawowe** warstwę wydajności i **50** obliczeniowe jednostki wspólne dla wszystkich baz danych hello powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="b48b6-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="b48b6-130">Możesz skalować możliwości obliczeniowe i Magazyn w górę lub w dół w zależności od potrzeb aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b48b6-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="b48b6-131">Konfigurowanie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="b48b6-131">Configure firewall rule</span></span>
<span data-ttu-id="b48b6-132">Utwórz bazę danych Azure, aby utworzyć regułę zapory poziomu serwera MySQL z hello az mysql reguły zapory serwera — polecenie.</span><span class="sxs-lookup"><span data-stu-id="b48b6-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="b48b6-133">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak **mysql** narzędzia wiersza polecenia lub MySQL Workbench tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b48b6-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="b48b6-134">Witaj poniższy przykład powoduje utworzenie reguły zapory dla zakresu adresów wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="b48b6-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="b48b6-135">Ten przykład przedstawia hello całego możliwe zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="b48b6-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="b48b6-136">Pobierz informacje o połączeniu hello</span><span class="sxs-lookup"><span data-stu-id="b48b6-136">Get hello connection information</span></span>

<span data-ttu-id="b48b6-137">tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b48b6-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="b48b6-138">wynik Hello jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b48b6-138">hello result is in JSON format.</span></span> <span data-ttu-id="b48b6-139">Zanotuj hello **fullyQualifiedDomainName** i **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="b48b6-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="b48b6-140">Połącz serwer toohello przy użyciu mysql</span><span class="sxs-lookup"><span data-stu-id="b48b6-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="b48b6-141">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour połączenia bazy danych platformy Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="b48b6-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="b48b6-142">W tym przykładzie polecenie hello jest:</span><span class="sxs-lookup"><span data-stu-id="b48b6-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="b48b6-143">Tworzenie pustej bazy danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-143">Create a blank database</span></span>
<span data-ttu-id="b48b6-144">Po wyświetleniu toohello podłączonego serwera, należy utworzyć pustą bazę danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="b48b6-145">W wierszu hello Uruchom hello następujące bazy danych polecenie tooswitch hello połączenia toothis nowo utworzone:</span><span class="sxs-lookup"><span data-stu-id="b48b6-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="b48b6-146">Tworzenie tabel w bazie danych hello</span><span class="sxs-lookup"><span data-stu-id="b48b6-146">Create tables in hello database</span></span>
<span data-ttu-id="b48b6-147">Teraz, gdy wiesz, jak tooconnect toohello Azure bazy danych dla bazy danych MySQL, firma Microsoft może przejść przez jak toocomplete niektóre podstawowe zadania.</span><span class="sxs-lookup"><span data-stu-id="b48b6-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="b48b6-148">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="b48b6-149">Teraz utworzyć tabelę, która przechowuje informacje dotyczące spisu.</span><span class="sxs-lookup"><span data-stu-id="b48b6-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="b48b6-150">Ładowanie danych do tabel hello</span><span class="sxs-lookup"><span data-stu-id="b48b6-150">Load data into hello tables</span></span>
<span data-ttu-id="b48b6-151">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="b48b6-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="b48b6-152">W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="b48b6-153">Masz teraz dwa wiersze przykładowych danych do tabeli hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b48b6-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="b48b6-154">Zapytania i Aktualizuj hello dane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="b48b6-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="b48b6-155">Wykonanie poniższych informacji tooretrieve zapytania z tabeli bazy danych hello hello.</span><span class="sxs-lookup"><span data-stu-id="b48b6-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="b48b6-156">Należy również zaktualizować hello dane w tabelach hello.</span><span class="sxs-lookup"><span data-stu-id="b48b6-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="b48b6-157">wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="b48b6-158">Przywracanie bazy danych tooa poprzedniego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="b48b6-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="b48b6-159">Załóżmy, że zostanie przypadkowo usunięte w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="b48b6-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="b48b6-160">Jest to coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="b48b6-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="b48b6-161">Bazy danych platformy Azure dla programu MySQL pozwala toogo tooany zapasowego punktu w czasie w hello ostatnio zapasowej too35 dni i przywrócić ten punkt w czasie tooa nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="b48b6-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="b48b6-162">Można użyć tego nowego serwera toorecover usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="b48b6-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="b48b6-163">Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="b48b6-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="b48b6-164">Witaj przywracania należy hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="b48b6-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="b48b6-165">Punkt przywracania: Wybierz w momencie po hello serwer został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="b48b6-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="b48b6-166">Musi być większa niż lub równa wartości kopii zapasowej najstarsze toohello źródłowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b48b6-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="b48b6-167">Serwer docelowy: Podaj nową nazwę serwera ma toorestore do</span><span class="sxs-lookup"><span data-stu-id="b48b6-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="b48b6-168">Serwer źródłowy: Podaj nazwę hello powitania serwera ma toorestore z</span><span class="sxs-lookup"><span data-stu-id="b48b6-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="b48b6-169">Lokalizacja: Nie można wybrać hello region, domyślnie jest taka sama jak powitania serwera źródłowego</span><span class="sxs-lookup"><span data-stu-id="b48b6-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="b48b6-170">toorestore powitania serwera i [tooa w momencie przywracania](./howto-restore-server-portal.md) przed hello tabeli został usunięty.</span><span class="sxs-lookup"><span data-stu-id="b48b6-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="b48b6-171">Przywracanie serwera tooa innego punktu w czasie tworzy zduplikowane nowy serwer jako hello oryginalny serwer określoną hello punktu w czasie, pod warunkiem, że w okresie przechowywania hello dla Twojego [warstwy usług](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="b48b6-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b48b6-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b48b6-172">Next Steps</span></span>
<span data-ttu-id="b48b6-173">W tym samouczku przedstawiono do:</span><span class="sxs-lookup"><span data-stu-id="b48b6-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b48b6-174">Utwórz bazę danych systemu Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="b48b6-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="b48b6-175">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="b48b6-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="b48b6-176">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bazy danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="b48b6-177">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="b48b6-177">Load sample data</span></span>
> * <span data-ttu-id="b48b6-178">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="b48b6-178">Query data</span></span>
> * <span data-ttu-id="b48b6-179">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-179">Update data</span></span>
> * <span data-ttu-id="b48b6-180">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="b48b6-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b48b6-181">Bazy danych platformy Azure dla programu MySQL — przykłady wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b48b6-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
