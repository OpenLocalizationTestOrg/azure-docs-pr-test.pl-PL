---
title: "Tworzenie bazy danych Azure dla PostgreSQL przy użyciu interfejsu wiersza polecenia Azure hello | Dokumentacja firmy Microsoft"
description: "Szybki start toocreate przewodnik i zarządzania nimi bazy danych Azure PostgreSQL serwera przy użyciu wiersza polecenia platformy Azure (interfejsu wiersza polecenia)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="d8d8e-103">Tworzenie bazy danych Azure dla PostgreSQL przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d8d8e-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="d8d8e-104">Bazy danych platformy Azure dla PostgreSQL jest zarządzana usługa, która pozwala toorun, zarządzanie i skalowania wysokiej dostępności PostgreSQL baz danych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="d8d8e-105">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="d8d8e-106">Ta opcja szybkiego startu przedstawia sposób toocreate Azure bazy danych dla serwera PostgreSQL w [grupy zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="d8d8e-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d8d8e-108">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d8d8e-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d8d8e-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d8d8e-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="d8d8e-111">Jeśli masz wiele subskrypcji, wybierz subskrypcję odpowiednie hello, naliczane hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="d8d8e-112">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="d8d8e-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d8d8e-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d8d8e-113">Create a resource group</span></span>

<span data-ttu-id="d8d8e-114">Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d8d8e-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d8d8e-116">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myresourcegroup` w hello `westus` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="d8d8e-117">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d8d8e-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="d8d8e-118">Utwórz [Azure bazy danych serwera PostgreSQL](overview.md) przy użyciu hello [utworzenie przez serwer postgres az](/cli/azure/postgres/server#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="d8d8e-119">Serwer zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="d8d8e-120">Witaj poniższy przykład tworzy serwer o nazwie `mypgserver-20170401` w grupie zasobów `myresourcegroup` z identyfikator logowania administratora serwera `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="d8d8e-121">Nazwa Hello serwera mapuje nazwę tooDNS i w związku z tym jest wymagana toobe globalnie unikatowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="d8d8e-122">SUBSTITUTE hello `<server_admin_password>` o własne wartości.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="d8d8e-123">Hello identyfikator logowania administratora serwera i hasło, które są określone w tym miejscu są wymagane toolog Server toohello i jej baz danych w dalszej części tego szybki start.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="d8d8e-124">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="d8d8e-125">Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="d8d8e-126">Witaj [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) baza danych jest domyślna baza danych przeznaczone do użytku przez użytkowników, narzędzia i aplikacje innych producentów.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="d8d8e-127">Konfigurowanie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="d8d8e-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="d8d8e-128">Utwórz regułę zapory poziomu serwera Azure PostgreSQL z hello [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d8d8e-129">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) lub [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="d8d8e-130">Można ustawić reguły zapory, która obejmuje IP zakresu toobe stanie tooconnect z sieci.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="d8d8e-131">Witaj poniższym przykładzie użyto [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) toocreate regułę zapory `AllowAllIps` zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="d8d8e-132">tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="d8d8e-133">Serwer Azure PostgreSQL komunikuje się przez port 5432.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="d8d8e-134">Podczas nawiązywania połączenia z sieci firmowej ruch wychodzący przez port 5432 może być blokowany przez zaporę sieciową.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d8d8e-135">Ma dział IT, otwórz port 5432 tooconnect tooyour bazy danych SQL Azure serwera.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="d8d8e-136">Pobierz informacje o połączeniu hello</span><span class="sxs-lookup"><span data-stu-id="d8d8e-136">Get hello connection information</span></span>

<span data-ttu-id="d8d8e-137">tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="d8d8e-138">wynik Hello jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-138">hello result is in JSON format.</span></span> <span data-ttu-id="d8d8e-139">Zanotuj hello **administratorLogin** i **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="d8d8e-140">Połącz tooPostgreSQL bazy danych przy użyciu psql</span><span class="sxs-lookup"><span data-stu-id="d8d8e-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="d8d8e-141">Jeśli komputer kliencki ma zainstalowany PostgreSQL, można użyć lokalnego wystąpienia programu [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="d8d8e-142">Użyjmy teraz hello psql narzędzia wiersza polecenia tooconnect toohello Azure PostgreSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="d8d8e-143">Uruchom następujące polecenie psql tooconnect tooan Azure bazy danych dla serwera PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="d8d8e-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="d8d8e-144">Na przykład następujące polecenie hello łączy toohello domyślna baza danych o nazwie **postgres** na serwerze PostgreSQL **mypgserver 20170401.postgres.database.azure.com** przy użyciu poświadczeń dostępu.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="d8d8e-145">Wprowadź hello `<server_admin_password>` wybrano po wyświetleniu monitu o hasło.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="d8d8e-146">Po przejściu toohello podłączonego serwera, należy utworzyć pustą bazę danych, w wierszu hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="d8d8e-147">W wierszu polecenia hello wykonania hello następujące polecenia tooswitch połączenia toohello nowo utworzone w bazie danych **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="d8d8e-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="d8d8e-148">Połącz tooPostgreSQL bazy danych przy użyciu pgAdmin</span><span class="sxs-lookup"><span data-stu-id="d8d8e-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="d8d8e-149">Serwer PostgreSQL tooAzure tooconnect przy użyciu hello graficznego interfejsu użytkownika narzędzia _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="d8d8e-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="d8d8e-150">Uruchamianie hello _pgAdmin_ aplikacji na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="d8d8e-151">Aplikację _pgAdmin_ można zainstalować ze strony http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="d8d8e-152">Wybierz **dodać nowy serwer** z hello **szybkie linki** menu.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="d8d8e-153">W hello **Utwórz — serwer** okno dialogowe **ogólne** wprowadź unikatową przyjazną nazwę dla serwera hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="d8d8e-154">Na przykład **Serwer Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="d8d8e-155">![Narzędzie pgAdmin — Tworzenie — Serwer](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="d8d8e-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="d8d8e-156">W hello **Utwórz — serwer** okno dialogowe **połączenia** karty:</span><span class="sxs-lookup"><span data-stu-id="d8d8e-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="d8d8e-157">Wprowadź nazwę FQDN serwera hello (na przykład **mypgserver 20170401.postgres.database.azure.com**) w hello **nazwę hosta / adres** pole.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="d8d8e-158">Wprowadź port 5432 do hello **portu** pole.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="d8d8e-159">Wprowadź hello **identyfikator logowania administratora serwera (user@mypgserver)** uzyskany wcześniej w tym Szybki Start i hasła podczas tworzenia powitania serwera na powitania **Username** i **hasło** pola odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="d8d8e-160">W polu **Tryb SSL** wybierz wartość **Wymagany**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="d8d8e-161">Domyślnie wszystkie serwery Azure PostgreSQL są tworzone z włączonym wymuszaniem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="d8d8e-162">tooturn Wyłącz wymuszanie protokołu SSL, zobacz szczegóły w [wymuszania SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="d8d8e-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![Narzędzie pgAdmin — Tworzenie — Serwer](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="d8d8e-164">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-164">Click **Save**.</span></span>
6.  <span data-ttu-id="d8d8e-165">W okienku po lewej stronie przeglądarki hello, rozwiń węzeł hello **grup serwerów**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="d8d8e-166">Wybierz swój serwer **Serwer Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="d8d8e-167">Wybierz hello **serwera** połączona, a następnie wybierz **baz danych** na jego podstawie.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="d8d8e-168">Kliknij prawym przyciskiem myszy **baz danych** tooCreate bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="d8d8e-169">Wybierz nazwę bazy danych **mypgsqldb** i hello właściciela go jako identyfikator logowania administratora serwera **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="d8d8e-170">Kliknij przycisk **zapisać** toocreate pustą bazę danych.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="d8d8e-171">W hello **przeglądarki**, rozwiń węzeł hello **serwerów** grupy.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="d8d8e-172">Rozwiń węzeł serwera hello utworzony i zobacz hello bazy danych **mypgsqldb** na jego podstawie.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="d8d8e-173">![Narzędzie pgAdmin — Tworzenie — Baza danych](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="d8d8e-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="d8d8e-174">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="d8d8e-174">Clean up resources</span></span>

<span data-ttu-id="d8d8e-175">Czyszczenie wszystkich zasobów utworzonego w szybkiego startu hello przez usunięcie hello [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8d8e-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="d8d8e-176">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="d8d8e-177">Jeśli planujesz toocontinue toowork kolejne Przewodniki Szybki Start, czy nie Oczyszczanie hello zasoby utworzone w tym Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="d8d8e-178">Jeśli nie planujesz toocontinue, użyj hello następujące kroki toodelete wszystkie zasoby utworzone przez tego szybkiego startu w hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="d8d8e-179">Jeśli chcesz tylko jeden serwer nowo utworzony hello toodelete, możesz uruchomić [usuwania serwera postgres az](/cli/azure/postgres/server#delete) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d8d8e-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="d8d8e-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8d8e-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d8d8e-181">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="d8d8e-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
