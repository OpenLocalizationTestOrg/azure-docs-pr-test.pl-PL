---
title: "Tworzenie serwera usługi Azure Database for PostgreSQL za pomocą interfejsu wiersza polecania platformy Azure | Microsoft Docs"
description: "Przewodnik Szybki start dotyczący tworzenia serwera usługi Azure Database for PostgreSQL i zarządzania nim przy użyciu interfejsu wiersza polecenia platformy Azure."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: d78243abc140c7b3f0b99bdf56821b7920568550
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-using-the-azure-cli"></a><span data-ttu-id="24067-103">Tworzenie serwera usługi Azure Database for PostgreSQL za pomocą interfejsu wiersza polecania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="24067-103">Create an Azure Database for PostgreSQL using the Azure CLI</span></span>
<span data-ttu-id="24067-104">Azure Database for PostgreSQL to usługa zarządzana, która umożliwia uruchamianie i skalowanie w chmurze baz danych PostgreSQL o wysokiej dostępności, a także zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="24067-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="24067-105">Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="24067-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="24067-106">W tym przewodniku Szybki start przedstawiono, jak utworzyć serwer usługi Azure Database for PostgreSQL w [grupie zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) za pomocą interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="24067-106">This quickstart shows you how to create an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the Azure CLI.</span></span>

<span data-ttu-id="24067-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="24067-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="24067-108">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="24067-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="24067-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="24067-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="24067-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24067-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="24067-111">Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w ramach której będą naliczane opłaty za ten zasób.</span><span class="sxs-lookup"><span data-stu-id="24067-111">If you have multiple subscriptions, choose the appropriate subscription in which the resource will be billed.</span></span> <span data-ttu-id="24067-112">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="24067-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="24067-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="24067-113">Create a resource group</span></span>

<span data-ttu-id="24067-114">Utwórz [grupę zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="24067-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="24067-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="24067-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="24067-116">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myresourcegroup` w lokalizacji `westus`.</span><span class="sxs-lookup"><span data-stu-id="24067-116">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="24067-117">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="24067-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="24067-118">Utwórz [serwer usługi Azure Database for PostgreSQL](overview.md) za pomocą polecenia [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="24067-118">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="24067-119">Serwer zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="24067-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="24067-120">W poniższym przykładzie zostanie utworzony serwer o nazwie `mypgserver-20170401` w grupie zasobów `myresourcegroup` z identyfikatorem logowania administratora serwera `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="24067-120">The following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="24067-121">Nazwa serwera jest mapowana na nazwę DNS i dlatego musi być globalnie unikatowa w ramach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="24067-121">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="24067-122">Zastąp zmienną `<server_admin_password>` swoją własną wartością.</span><span class="sxs-lookup"><span data-stu-id="24067-122">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="24067-123">Login i hasło administratora serwera określone w tym miejscu będą wymagane do logowania do serwera i jego baz danych w późniejszej części tego przewodnika Szybki start.</span><span class="sxs-lookup"><span data-stu-id="24067-123">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="24067-124">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="24067-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="24067-125">Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze.</span><span class="sxs-lookup"><span data-stu-id="24067-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="24067-126">Baza danych [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) to domyślna baza danych przeznaczona do użycia dla użytkowników oraz na potrzeby narzędzi i aplikacji innych firm.</span><span class="sxs-lookup"><span data-stu-id="24067-126">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="24067-127">Konfigurowanie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="24067-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="24067-128">Utwórz regułę zapory na poziomie serwera Azure PostgreSQL za pomocą polecenia [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="24067-128">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="24067-129">Reguła zapory na poziomie serwera pozwala aplikacji zewnętrznej, takiej jak narzędzie [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) lub [PgAdmin](https://www.pgadmin.org/), na nawiązywanie połączeń z Twoim serwerem przez zaporę usługi Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="24067-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="24067-130">Możesz ustawić regułę zapory uwzględniającą zakres adresów IP, aby mieć możliwość nawiązywania połączeń z Twojej sieci.</span><span class="sxs-lookup"><span data-stu-id="24067-130">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="24067-131">W poniższym przykładzie użyto polecenia [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) w celu utworzenia reguły zapory `AllowAllIps` dla zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="24067-131">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="24067-132">Aby otworzyć wszystkie adresy IP, użyj wartości 0.0.0.0 jako początkowego adresu IP i wartości 255.255.255.255 jako adresu końcowego.</span><span class="sxs-lookup"><span data-stu-id="24067-132">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="24067-133">Serwer Azure PostgreSQL komunikuje się przez port 5432.</span><span class="sxs-lookup"><span data-stu-id="24067-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="24067-134">Podczas nawiązywania połączenia z sieci firmowej ruch wychodzący przez port 5432 może być blokowany przez zaporę sieciową.</span><span class="sxs-lookup"><span data-stu-id="24067-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="24067-135">Aby było możliwe nawiązywanie połączenia z serwerem usługi Azure SQL Database, poproś dział IT o otwarcie portu 5432.</span><span class="sxs-lookup"><span data-stu-id="24067-135">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>

## <a name="get-the-connection-information"></a><span data-ttu-id="24067-136">Uzyskiwanie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="24067-136">Get the connection information</span></span>

<span data-ttu-id="24067-137">Aby nawiązać połączenie z serwerem, musisz podać informacje o hoście i poświadczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="24067-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="24067-138">Wynik jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="24067-138">The result is in JSON format.</span></span> <span data-ttu-id="24067-139">Zanotuj wartości **administratorLogin** i **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="24067-139">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-postgresql-database-using-psql"></a><span data-ttu-id="24067-140">Nawiązywanie połączenia z bazą danych PostgreSQL za pomocą narzędzia psql</span><span class="sxs-lookup"><span data-stu-id="24067-140">Connect to PostgreSQL database using psql</span></span>

<span data-ttu-id="24067-141">Jeśli na Twoim komputerze klienckim jest zainstalowany program PostgreSQL, możesz użyć lokalnego wystąpienia narzędzia [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), aby nawiązać połączenie z serwerem Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="24067-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="24067-142">Użyj teraz narzędzia wiersza polecenia psql, aby nawiązać połączenie z serwerem Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="24067-142">Let's now use the psql command-line utility to connect to the Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="24067-143">Uruchom poniższe polecenie psql w celu nawiązania połączenia z serwerem usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="24067-143">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="24067-144">Na przykład poniższe polecenie nawiązuje połączenie z domyślną bazą danych o nazwie **postgres** na Twoim serwerze PostgreSQL **mypgserver-20170401.postgres.database.azure.com** za pomocą poświadczeń dostępu.</span><span class="sxs-lookup"><span data-stu-id="24067-144">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="24067-145">Gdy zostanie wyświetlony monit o podanie hasła, wprowadź wybrane hasło `<server_admin_password>`.</span><span class="sxs-lookup"><span data-stu-id="24067-145">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="24067-146">Po nawiązaniu połączenia z serwerem utwórz pustą bazę danych za pomocą wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="24067-146">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="24067-147">W wierszu polecenia wykonaj poniższe polecenie, aby przełączyć połączenie na nowo utworzoną bazę danych **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="24067-147">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-to-postgresql-database-using-pgadmin"></a><span data-ttu-id="24067-148">Nawiązywanie połączenia z bazą danych PostgreSQL za pomocą narzędzia pgAdmin</span><span class="sxs-lookup"><span data-stu-id="24067-148">Connect to PostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="24067-149">Aby nawiązać połączenie z serwerem usługi Azure PostgreSQL za pomocą narzędzia z graficznym interfejsem użytkownika _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="24067-149">To connect to Azure PostgreSQL server using the GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="24067-150">Uruchom aplikację _pgAdmin_ na swoim komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="24067-150">Launch the _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="24067-151">Aplikację _pgAdmin_ można zainstalować ze strony http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="24067-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="24067-152">Wybierz pozycję **Dodaj nowy serwer** w menu **Szybkie linki**.</span><span class="sxs-lookup"><span data-stu-id="24067-152">Choose **Add New Server** from the **Quick Links** menu.</span></span>
3.  <span data-ttu-id="24067-153">W oknie dialogowym **Tworzenie — Serwer** na karcie **Ogólne** wprowadź unikatową przyjazną nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="24067-153">In the **Create - Server** dialog box **General** tab, enter a unique friendly Name for the server.</span></span> <span data-ttu-id="24067-154">Na przykład **Serwer Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="24067-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="24067-155">![Narzędzie pgAdmin — Tworzenie — Serwer](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="24067-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="24067-156">W oknie dialogowym **Tworzenie — Serwer** na karcie **Połączenie**:</span><span class="sxs-lookup"><span data-stu-id="24067-156">In the **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="24067-157">Wprowadź w pełni kwalifikowaną nazwę serwera (na przykład **mypgserver-20170401.postgres.database.azure.com**) w polu **Nazwa/adres hosta**.</span><span class="sxs-lookup"><span data-stu-id="24067-157">Enter the fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in the **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="24067-158">Wprowadź port 5432 w polu **Port**.</span><span class="sxs-lookup"><span data-stu-id="24067-158">Enter port 5432 into the **Port** box.</span></span> 
    - <span data-ttu-id="24067-159">Wprowadź **identyfikator logowania administratora serwera (user@mypgserver)** uzyskany wcześniej w tym przewodniku Szybki start oraz hasło wprowadzone podczas tworzenia serwera odpowiednio w polach **Użytkownik** i **Hasło**.</span><span class="sxs-lookup"><span data-stu-id="24067-159">Enter the **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created the server into the **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="24067-160">W polu **Tryb SSL** wybierz wartość **Wymagany**.</span><span class="sxs-lookup"><span data-stu-id="24067-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="24067-161">Domyślnie wszystkie serwery Azure PostgreSQL są tworzone z włączonym wymuszaniem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="24067-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="24067-162">Aby wyłączyć wymuszanie protokołu SSL, zobacz szczegółowe informacje w artykule [Wymuszanie protokołu SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="24067-162">To turn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![Narzędzie pgAdmin — Tworzenie — Serwer](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="24067-164">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="24067-164">Click **Save**.</span></span>
6.  <span data-ttu-id="24067-165">W lewym okienku Browser (Przeglądarka) rozwiń węzeł **Server Groups** (Grupy serwerów).</span><span class="sxs-lookup"><span data-stu-id="24067-165">In the Browser left pane, expand the **Server Groups**.</span></span> <span data-ttu-id="24067-166">Wybierz swój serwer **Serwer Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="24067-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="24067-167">Wybierz **serwer**, z którym nawiązano połączenie, a następnie wybierz w jego obszarze pozycję **Databases** (Bazy danych).</span><span class="sxs-lookup"><span data-stu-id="24067-167">Choose the **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="24067-168">Kliknij prawym przyciskiem myszy pozycję **Databases** (Bazy danych), aby utworzyć bazę danych.</span><span class="sxs-lookup"><span data-stu-id="24067-168">Right-click on **Databases** to Create a Database.</span></span>
9.  <span data-ttu-id="24067-169">Wybierz nazwę bazy danych **mypgsqldb** oraz jej właściciela: identyfikator logowania administratora serwera **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="24067-169">Choose a database name **mypgsqldb** and the owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="24067-170">Kliknij przycisk **Zapisz**, aby utworzyć pustą bazę danych.</span><span class="sxs-lookup"><span data-stu-id="24067-170">Click **Save** to create a blank database.</span></span>
11. <span data-ttu-id="24067-171">W oknie **Przeglądarka** rozwiń grupę **Serwery**.</span><span class="sxs-lookup"><span data-stu-id="24067-171">In the **Browser**, expand the **Servers** group.</span></span> <span data-ttu-id="24067-172">Rozwiń utworzony serwer. Będzie widoczna baza danych **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="24067-172">Expand the server you created, and see the database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="24067-173">![Narzędzie pgAdmin — Tworzenie — Baza danych](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="24067-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="24067-174">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="24067-174">Clean up resources</span></span>

<span data-ttu-id="24067-175">Wyczyść wszystkie zasoby utworzone w tym przewodniku Szybki start, usuwając [grupę zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24067-175">Clean up all resources you created in the quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="24067-176">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="24067-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="24067-177">Jeśli planujesz kontynuować pracę z kolejnymi przewodnikami Szybki start, nie usuwaj zasobów utworzonych w tym przewodniku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="24067-177">If you plan to continue on to work with subsequent quickstarts, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="24067-178">Jeśli nie planujesz kontynuować pracy, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone za pomocą interfejsu wiersza polecenia platformy Azure w ramach tego przewodnika Szybki start.</span><span class="sxs-lookup"><span data-stu-id="24067-178">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="24067-179">Jeśli po prostu chcesz usunąć jeden z nowo utworzonych serwerów, możesz uruchomić polecenie [az postgres server delete](/cli/azure/postgres/server#delete).</span><span class="sxs-lookup"><span data-stu-id="24067-179">If you just would like to delete the one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="24067-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24067-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="24067-181">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="24067-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
