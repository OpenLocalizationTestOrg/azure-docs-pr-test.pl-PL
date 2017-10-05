---
title: "Szybki start: tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecania platformy Azure | Microsoft Docs"
description: "W tym przewodniku Szybki start opisano, jak utworzyć serwer usługi Azure Database for MySQL w grupie zasobów platformy Azure za pomocą interfejsu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: 04fc441aee7a4c8adc4f02d5e51b2d9e64400f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="9080b-103">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9080b-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="9080b-104">W tym przewodniku Szybki start opisano, jak utworzyć serwer usługi Azure Database for MySQL w grupie zasobów platformy Azure za pomocą interfejsu wiersza polecenia platformy Azure w czasie około pięciu minut.</span><span class="sxs-lookup"><span data-stu-id="9080b-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="9080b-105">Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="9080b-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="9080b-106">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="9080b-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9080b-107">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9080b-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9080b-108">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="9080b-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="9080b-109">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9080b-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="9080b-110">Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w której zasób istnieje lub dla której są za niego naliczane opłaty.</span><span class="sxs-lookup"><span data-stu-id="9080b-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="9080b-111">Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="9080b-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="9080b-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="9080b-112">Create a resource group</span></span>
<span data-ttu-id="9080b-113">Utwórz [grupę zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) za pomocą polecenia [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9080b-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="9080b-114">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="9080b-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="9080b-115">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myresourcegroup` w lokalizacji `westus`.</span><span class="sxs-lookup"><span data-stu-id="9080b-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="9080b-116">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="9080b-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="9080b-117">Utwórz serwer usługi Azure Database for MySQL za pomocą polecenia **az mysql server create**.</span><span class="sxs-lookup"><span data-stu-id="9080b-117">Create an Azure Database for MySQL server with the **az mysql server create** command.</span></span> <span data-ttu-id="9080b-118">Serwer umożliwia zarządzanie wieloma bazami danych.</span><span class="sxs-lookup"><span data-stu-id="9080b-118">A server can manage multiple databases.</span></span> <span data-ttu-id="9080b-119">Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.</span><span class="sxs-lookup"><span data-stu-id="9080b-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="9080b-120">W poniższym przykładzie w regionie `westus` w grupie zasobów `myresourcegroup` jest tworzony serwer usługi Azure Database for MySQL o nazwie `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="9080b-120">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="9080b-121">Serwer ma identyfikator logowania administratora o nazwie `myadmin` i hasło `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="9080b-121">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="9080b-122">Serwer jest tworzony w ramach warstwy wydajności **Podstawowa** i z użyciem **50** jednostek obliczeniowych współdzielonych między wszystkimi bazami danych na tym serwerze.</span><span class="sxs-lookup"><span data-stu-id="9080b-122">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="9080b-123">Możesz skalować zasoby obliczeniowe i magazyn w górę lub w dół w zależności od potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9080b-123">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="9080b-124">Konfigurowanie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="9080b-124">Configure firewall rule</span></span>
<span data-ttu-id="9080b-125">Utwórz regułę zapory na poziomie serwera usługi Azure Database for MySQL za pomocą polecenia **az mysql server firewall-rule create**.</span><span class="sxs-lookup"><span data-stu-id="9080b-125">Create an Azure Database for MySQL server-level firewall rule using the **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="9080b-126">Reguła zapory na poziomie serwera pozwala aplikacji zewnętrznej, takiej jak narzędzie wiersza polecenia **mysql.exe** lub program MySQL Workbench, na nawiązywanie połączeń z Twoim serwerem przez zaporę usługi Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="9080b-126">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="9080b-127">W poniższym przykładzie jest tworzona reguła zapory dla wstępnie zdefiniowanego zakresu adresów, który w tym przypadku jest całym możliwym zakresem adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9080b-127">The following example creates a firewall rule for a predefined address range, which in this example is the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="9080b-128">Konfigurowanie ustawień SSL</span><span class="sxs-lookup"><span data-stu-id="9080b-128">Configure SSL settings</span></span>
<span data-ttu-id="9080b-129">Domyślnie połączenia SSL między Twoim serwerem i aplikacjami klienckimi są wymuszane.</span><span class="sxs-lookup"><span data-stu-id="9080b-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="9080b-130">Zapewnia to bezpieczeństwo danych „w ruchu” przez szyfrowanie strumienia danych przesyłanych przez Internet.</span><span class="sxs-lookup"><span data-stu-id="9080b-130">This ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span>  <span data-ttu-id="9080b-131">Aby uprościć ten przewodnik Szybki start, wyłączamy połączenia SSL dla Twojego serwera.</span><span class="sxs-lookup"><span data-stu-id="9080b-131">To make this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="9080b-132">Nie jest to zalecane w przypadku serwerów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="9080b-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="9080b-133">Aby uzyskać więcej informacji, zobacz [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL (Konfigurowanie łączności SSL w aplikacji w celu bezpiecznego nawiązywania połączeń z usługą Azure Database for MySQL)](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9080b-133">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="9080b-134">W poniższym przykładzie jest wyłączane wymuszanie protokołu SSL na Twoim serwerze MySQL.</span><span class="sxs-lookup"><span data-stu-id="9080b-134">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="9080b-135">Uzyskiwanie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="9080b-135">Get the connection information</span></span>

<span data-ttu-id="9080b-136">Aby nawiązać połączenie z serwerem, musisz podać informacje o hoście i poświadczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="9080b-136">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="9080b-137">Wynik jest w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="9080b-137">The result is in JSON format.</span></span> <span data-ttu-id="9080b-138">Zanotuj wartości **fullyQualifiedDomainName** i **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="9080b-138">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="9080b-139">Nawiązywanie połączenia z serwerem za pomocą narzędzia wiersza polecenia mysql.exe</span><span class="sxs-lookup"><span data-stu-id="9080b-139">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="9080b-140">Nawiąż połączenia z serwerem za pomocą narzędzia wiersza polecenia **mysql.exe**.</span><span class="sxs-lookup"><span data-stu-id="9080b-140">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="9080b-141">Program MySQL możesz pobrać [stąd](https://dev.mysql.com/downloads/) i zainstalować go na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="9080b-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="9080b-142">Zamiast tego możesz też kliknąć przycisk **Wypróbuj** przy przykładach kodu lub przycisk `>_` na pasku narzędzi po prawej stronie u góry w witrynie Azure Portal i uruchomić usługę **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="9080b-142">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="9080b-143">Wpisz kolejne polecenia:</span><span class="sxs-lookup"><span data-stu-id="9080b-143">Type the next commands:</span></span> 

1. <span data-ttu-id="9080b-144">Nawiąż połączenie z serwerem za pomocą narzędzia wiersza polecenia **mysql**:</span><span class="sxs-lookup"><span data-stu-id="9080b-144">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="9080b-145">Wyświetl stan serwera:</span><span class="sxs-lookup"><span data-stu-id="9080b-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="9080b-146">Jeśli wszystko pójdzie dobrze, narzędzie wiersza polecenia powinno zwrócić następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="9080b-146">If everything goes well, the command-line tool should output the following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

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
> <span data-ttu-id="9080b-147">Aby zapoznać się z dodatkowymi poleceniami, zobacz [MySQL 5.7 Reference Manual - Chapter 4.5.1 (Podręcznik programu MySQL 5.7 — Rozdział 4.5.1)](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="9080b-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="9080b-148">Nawiązywanie połączenia z serwerem za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="9080b-148">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="9080b-149">Uruchom aplikację MySQL Workbench na swoim komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="9080b-149">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="9080b-150">Aplikację MySQL Workbench możesz pobrać i zainstalować [stąd](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="9080b-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="9080b-151">W oknie dialogowym **Konfigurowanie nowego połączenia** wprowadź poniższe informacje na karcie **Parametry**:</span><span class="sxs-lookup"><span data-stu-id="9080b-151">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![konfigurowanie nowego połączenia](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="9080b-153">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="9080b-153">**Setting**</span></span> | <span data-ttu-id="9080b-154">**Sugerowana wartość**</span><span class="sxs-lookup"><span data-stu-id="9080b-154">**Suggested Value**</span></span> | <span data-ttu-id="9080b-155">**Opis**</span><span class="sxs-lookup"><span data-stu-id="9080b-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="9080b-156">Nazwa połączenia</span><span class="sxs-lookup"><span data-stu-id="9080b-156">Connection Name</span></span> | <span data-ttu-id="9080b-157">Moje połączenie</span><span class="sxs-lookup"><span data-stu-id="9080b-157">My Connection</span></span> | <span data-ttu-id="9080b-158">Podaj etykietę dla tego połączenia (może to być dowolny tekst)</span><span class="sxs-lookup"><span data-stu-id="9080b-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="9080b-159">Metoda połączenia</span><span class="sxs-lookup"><span data-stu-id="9080b-159">Connection Method</span></span> | <span data-ttu-id="9080b-160">wybierz opcję Standardowa (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="9080b-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="9080b-161">Użyj protokołu TCP/IP do nawiązania połączenia z bazą danych platformy Azure Database dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="9080b-161">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="9080b-162">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="9080b-162">Hostname</span></span> | <span data-ttu-id="9080b-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="9080b-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="9080b-164">Wcześniej zanotowana nazwa serwera.</span><span class="sxs-lookup"><span data-stu-id="9080b-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="9080b-165">Port</span><span class="sxs-lookup"><span data-stu-id="9080b-165">Port</span></span> | <span data-ttu-id="9080b-166">3306</span><span class="sxs-lookup"><span data-stu-id="9080b-166">3306</span></span> | <span data-ttu-id="9080b-167">Używany jest domyślny port dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="9080b-167">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="9080b-168">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="9080b-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="9080b-169">Identyfikator logowania administratora serwera zanotowany przez Ciebie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9080b-169">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="9080b-170">Hasło</span><span class="sxs-lookup"><span data-stu-id="9080b-170">Password</span></span> | **** | <span data-ttu-id="9080b-171">Użyj hasła do konta administratora, które zostało ustawione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9080b-171">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="9080b-172">Kliknij przycisk **Testuj połączenie**, aby sprawdzić, czy wszystkie parametry zostały prawidłowo skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="9080b-172">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="9080b-173">Teraz możesz kliknąć połączenie, aby pomyślnie nawiązać połączenie z serwerem.</span><span class="sxs-lookup"><span data-stu-id="9080b-173">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9080b-174">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="9080b-174">Clean up resources</span></span>
<span data-ttu-id="9080b-175">Jeśli te zasoby nie są Ci potrzebne do pracy z innym przewodnikiem Szybki start lub samouczkiem, możesz je usunąć, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9080b-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="9080b-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9080b-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9080b-177">Projektowanie bazy danych MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9080b-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
