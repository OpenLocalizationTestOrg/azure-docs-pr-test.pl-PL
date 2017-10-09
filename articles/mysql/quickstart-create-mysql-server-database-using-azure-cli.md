---
title: "Szybki start: tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecania platformy Azure | Microsoft Docs"
description: "Ta opcja szybkiego startu w tym artykule opisano sposób toouse hello Azure CLI toocreate bazy danych Azure MySQL serwera w ramach grupy zasobów platformy Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="82a1a-103">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="82a1a-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="82a1a-104">Ta opcja szybkiego startu w tym artykule opisano sposób toouse hello Azure CLI toocreate bazy danych Azure MySQL serwera w ramach grupy zasobów platformy Azure w ciągu około pięciu minut.</span><span class="sxs-lookup"><span data-stu-id="82a1a-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="82a1a-105">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="82a1a-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="82a1a-106">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="82a1a-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="82a1a-107">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="82a1a-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="82a1a-108">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="82a1a-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="82a1a-109">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82a1a-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="82a1a-110">Jeśli masz wiele subskrypcji, wybierz hello odpowiednie subskrypcji, w którym hello zasobów istnieje lub jest on rozliczany dla.</span><span class="sxs-lookup"><span data-stu-id="82a1a-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="82a1a-111">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="82a1a-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="82a1a-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="82a1a-112">Create a resource group</span></span>
<span data-ttu-id="82a1a-113">Utwórz [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) przy użyciu hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="82a1a-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="82a1a-114">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="82a1a-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="82a1a-115">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myresourcegroup` w hello `westus` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="82a1a-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="82a1a-116">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="82a1a-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="82a1a-117">Tworzenie bazy danych Azure MySQL serwera z hello **utworzenie przez serwer mysql az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="82a1a-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="82a1a-118">Serwer umożliwia zarządzanie wieloma bazami danych.</span><span class="sxs-lookup"><span data-stu-id="82a1a-118">A server can manage multiple databases.</span></span> <span data-ttu-id="82a1a-119">Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.</span><span class="sxs-lookup"><span data-stu-id="82a1a-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="82a1a-120">Witaj poniższy przykład tworzy Azure bazę danych MySQL serwera znajduje się w `westus` w grupie zasobów hello `myresourcegroup` o nazwie `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="82a1a-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="82a1a-121">powitania serwera zawiera dziennik administratora w nazwie `myadmin` i hasło `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="82a1a-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="82a1a-122">Serwer Hello jest tworzony z **podstawowe** warstwę wydajności i **50** obliczeniowe jednostki wspólne dla wszystkich baz danych hello powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="82a1a-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="82a1a-123">Możesz skalować możliwości obliczeniowe i Magazyn w górę lub w dół w zależności od potrzeb aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="82a1a-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="82a1a-124">Konfigurowanie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="82a1a-124">Configure firewall rule</span></span>
<span data-ttu-id="82a1a-125">Utwórz bazę danych MySQL reguły zapory poziomu serwera przy użyciu hello Azure **az mysql reguły zapory serwera — Utwórz** polecenia.</span><span class="sxs-lookup"><span data-stu-id="82a1a-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="82a1a-126">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak hello **mysql.exe** narzędzia wiersza polecenia lub MySQL Workbench tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="82a1a-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="82a1a-127">Witaj poniższy przykład powoduje utworzenie reguły zapory dla zakresu adresów wstępnie zdefiniowanych, czyli w tym przykładzie hello całego możliwe zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="82a1a-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="82a1a-128">Konfigurowanie ustawień SSL</span><span class="sxs-lookup"><span data-stu-id="82a1a-128">Configure SSL settings</span></span>
<span data-ttu-id="82a1a-129">Domyślnie połączenia SSL między Twoim serwerem i aplikacjami klienckimi są wymuszane.</span><span class="sxs-lookup"><span data-stu-id="82a1a-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="82a1a-130">Dzięki temu zabezpieczeń "w ruchu" danych przez szyfrowanie hello strumienia danych za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="82a1a-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="82a1a-131">toomake to szybki start łatwiej, możemy wyłączyć połączeń SSL serwera.</span><span class="sxs-lookup"><span data-stu-id="82a1a-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="82a1a-132">Nie jest to zalecane w przypadku serwerów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="82a1a-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="82a1a-133">Aby uzyskać więcej informacji, zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="82a1a-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="82a1a-134">Witaj poniższy przykład powoduje wyłączenie wymuszenie SSL na serwerze programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="82a1a-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="82a1a-135">Pobierz informacje o połączeniu hello</span><span class="sxs-lookup"><span data-stu-id="82a1a-135">Get hello connection information</span></span>

<span data-ttu-id="82a1a-136">tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="82a1a-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="82a1a-137">wynik Hello jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="82a1a-137">hello result is in JSON format.</span></span> <span data-ttu-id="82a1a-138">Zanotuj hello **fullyQualifiedDomainName** i **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="82a1a-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="82a1a-139">Połącz serwer toohello za pomocą narzędzia wiersza polecenia mysql.exe hello</span><span class="sxs-lookup"><span data-stu-id="82a1a-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="82a1a-140">Połącz przy użyciu powitania serwera tooyour **mysql.exe** narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="82a1a-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="82a1a-141">Program MySQL możesz pobrać [stąd](https://dev.mysql.com/downloads/) i zainstalować go na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="82a1a-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="82a1a-142">Zamiast tego możesz również kliknąć pozycję hello **spróbuj on** znajdującego się na przykłady kodu lub hello `>_` przycisk hello górnym prawym pasku narzędzi w hello portalu Azure i uruchamiania hello **powłoki chmury Azure**.</span><span class="sxs-lookup"><span data-stu-id="82a1a-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="82a1a-143">Wpisz hello następnego polecenia:</span><span class="sxs-lookup"><span data-stu-id="82a1a-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="82a1a-144">Połącz, używając serwera toohello **mysql** narzędzia wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="82a1a-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="82a1a-145">Wyświetl stan serwera:</span><span class="sxs-lookup"><span data-stu-id="82a1a-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="82a1a-146">Jeśli wszystko odbędzie się poprawnie, narzędzia wiersza polecenia hello powinien output hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="82a1a-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="82a1a-147">Aby zapoznać się z dodatkowymi poleceniami, zobacz [MySQL 5.7 Reference Manual - Chapter 4.5.1 (Podręcznik programu MySQL 5.7 — Rozdział 4.5.1)](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="82a1a-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="82a1a-148">Połącz przy użyciu narzędzia Workbench MySQL graficznego interfejsu użytkownika hello serwer toohello</span><span class="sxs-lookup"><span data-stu-id="82a1a-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="82a1a-149">Uruchom program hello MySQL Workbench aplikacji na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="82a1a-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="82a1a-150">Aplikację MySQL Workbench możesz pobrać i zainstalować [stąd](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="82a1a-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="82a1a-151">W hello **instalacji nowego połączenia** okna dialogowego wprowadź hello następujących informacji **parametry** karty:</span><span class="sxs-lookup"><span data-stu-id="82a1a-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![konfigurowanie nowego połączenia](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="82a1a-153">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="82a1a-153">**Setting**</span></span> | <span data-ttu-id="82a1a-154">**Sugerowana wartość**</span><span class="sxs-lookup"><span data-stu-id="82a1a-154">**Suggested Value**</span></span> | <span data-ttu-id="82a1a-155">**Opis**</span><span class="sxs-lookup"><span data-stu-id="82a1a-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="82a1a-156">Nazwa połączenia</span><span class="sxs-lookup"><span data-stu-id="82a1a-156">Connection Name</span></span> | <span data-ttu-id="82a1a-157">Moje połączenie</span><span class="sxs-lookup"><span data-stu-id="82a1a-157">My Connection</span></span> | <span data-ttu-id="82a1a-158">Podaj etykietę dla tego połączenia (może to być dowolny tekst)</span><span class="sxs-lookup"><span data-stu-id="82a1a-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="82a1a-159">Metoda połączenia</span><span class="sxs-lookup"><span data-stu-id="82a1a-159">Connection Method</span></span> | <span data-ttu-id="82a1a-160">wybierz opcję Standardowa (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="82a1a-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="82a1a-161">Użyj protokołu TCP/IP w tooconnect tooAzure bazy danych dla programu MySQL ></span><span class="sxs-lookup"><span data-stu-id="82a1a-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="82a1a-162">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="82a1a-162">Hostname</span></span> | <span data-ttu-id="82a1a-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="82a1a-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="82a1a-164">Wcześniej zanotowana nazwa serwera.</span><span class="sxs-lookup"><span data-stu-id="82a1a-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="82a1a-165">Port</span><span class="sxs-lookup"><span data-stu-id="82a1a-165">Port</span></span> | <span data-ttu-id="82a1a-166">3306</span><span class="sxs-lookup"><span data-stu-id="82a1a-166">3306</span></span> | <span data-ttu-id="82a1a-167">domyślny port MySQL Hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="82a1a-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="82a1a-168">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="82a1a-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="82a1a-169">Witaj identyfikator logowania administratora serwera zanotowaną wcześniej.</span><span class="sxs-lookup"><span data-stu-id="82a1a-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="82a1a-170">Hasło</span><span class="sxs-lookup"><span data-stu-id="82a1a-170">Password</span></span> | **** | <span data-ttu-id="82a1a-171">Użyj hello hasło konta administratora, przez skonfigurowane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="82a1a-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="82a1a-172">Kliknij przycisk **Testuj połączenie** tootest, jeśli wszystkie parametry są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="82a1a-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="82a1a-173">Teraz, możesz kliknąć połączenia hello toosuccessfully połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="82a1a-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="82a1a-174">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="82a1a-174">Clean up resources</span></span>
<span data-ttu-id="82a1a-175">Jeśli nie potrzebujesz tych zasobów innym Szybki Start/samouczek, usunąć je, wykonując następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="82a1a-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="82a1a-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82a1a-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82a1a-177">Projektowanie bazy danych MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="82a1a-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
