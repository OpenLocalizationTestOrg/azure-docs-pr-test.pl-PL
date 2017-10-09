---
title: aaaDesign pierwszy Azure bazy danych dla bazy danych MySQL - portalu Azure | Dokumentacja firmy Microsoft
description: "Ten samouczek wyjaśnia sposób toocreate i zarządzanie bazą danych Azure MySQL serwera i bazy danych przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="0c433-103">Projektowanie pierwszej bazy danych Azure, aby baza danych MySQL</span><span class="sxs-lookup"><span data-stu-id="0c433-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="0c433-104">Bazy danych platformy Azure dla programu MySQL jest zarządzana usługa, która pozwala toorun, zarządzanie i skalowania wysokiej dostępności baz danych MySQL w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="0c433-105">Przy użyciu hello portalu Azure, można łatwo zarządzać serwerem i projektowanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0c433-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="0c433-106">W tym samouczku użyjesz hello toolearn portalu Azure, jak do:</span><span class="sxs-lookup"><span data-stu-id="0c433-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0c433-107">Utwórz bazę danych systemu Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="0c433-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="0c433-108">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="0c433-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="0c433-109">Użyj mysql narzędzia wiersza polecenia toocreate bazy danych</span><span class="sxs-lookup"><span data-stu-id="0c433-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="0c433-110">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="0c433-110">Load sample data</span></span>
> * <span data-ttu-id="0c433-111">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="0c433-111">Query data</span></span>
> * <span data-ttu-id="0c433-112">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="0c433-112">Update data</span></span>
> * <span data-ttu-id="0c433-113">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="0c433-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="0c433-114">Zaloguj się toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0c433-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="0c433-115">Otwórz przeglądarkę sieci web Ulubione, a następnie odwiedź hello [portalu Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0c433-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0c433-116">Wprowadź toosign Twoje poświadczenia w portalu toohello.</span><span class="sxs-lookup"><span data-stu-id="0c433-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="0c433-117">Widok domyślny Hello jest pulpit nawigacyjny usługi.</span><span class="sxs-lookup"><span data-stu-id="0c433-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="0c433-118">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="0c433-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="0c433-119">Serwer usługi Azure Database for MySQL jest tworzony za pomocą zdefiniowanego zestawu [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0c433-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="0c433-120">Serwer Hello jest tworzony w [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="0c433-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="0c433-121">Przejdź za**baz danych** > **bazy danych Azure dla programu MySQL**.</span><span class="sxs-lookup"><span data-stu-id="0c433-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="0c433-122">Jeśli nie można znaleźć serwera MySQL w obszarze **baz danych** kategorii, kliknij przycisk **zobaczyć wszystkie** tooshow wszystkie dostępne usługi bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0c433-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="0c433-123">Możesz także wpisać **bazy danych Azure dla programu MySQL** w tooquickly pole wyszukiwania hello znaleźć hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0c433-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="0c433-124">![TooMySQL Nawigacja 2-1](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="0c433-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="0c433-125">Kliknij przycisk **bazy danych Azure dla programu MySQL** Kafelek, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0c433-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="0c433-126">W naszym przykładzie wypełnić hello Azure bazy danych MySQL formularza z hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="0c433-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="0c433-127">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="0c433-127">**Setting**</span></span> | <span data-ttu-id="0c433-128">**Sugerowana wartość**</span><span class="sxs-lookup"><span data-stu-id="0c433-128">**Suggested value**</span></span> | <span data-ttu-id="0c433-129">**Opis pola**</span><span class="sxs-lookup"><span data-stu-id="0c433-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="0c433-130">*Nazwa serwera*</span><span class="sxs-lookup"><span data-stu-id="0c433-130">*Server name*</span></span> | <span data-ttu-id="0c433-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="0c433-131">myserver4demo</span></span>  | <span data-ttu-id="0c433-132">Nazwa serwera ma toobe globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="0c433-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="0c433-133">*Subskrypcja*</span><span class="sxs-lookup"><span data-stu-id="0c433-133">*Subscription*</span></span> | <span data-ttu-id="0c433-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="0c433-134">mysubscription</span></span> | <span data-ttu-id="0c433-135">Wybierz subskrypcję z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="0c433-136">*Grupa zasobów*</span><span class="sxs-lookup"><span data-stu-id="0c433-136">*Resource group*</span></span> | <span data-ttu-id="0c433-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="0c433-137">myresourcegroup</span></span> | <span data-ttu-id="0c433-138">Utwórz grupę zasobów lub wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="0c433-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="0c433-139">*Identyfikator logowania administratora serwera*</span><span class="sxs-lookup"><span data-stu-id="0c433-139">*Server admin login*</span></span> | <span data-ttu-id="0c433-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="0c433-140">myadmin</span></span> | <span data-ttu-id="0c433-141">Konfiguracja nazwy konta administratora.</span><span class="sxs-lookup"><span data-stu-id="0c433-141">Setup admin account name.</span></span> |
| <span data-ttu-id="0c433-142">*Hasło*</span><span class="sxs-lookup"><span data-stu-id="0c433-142">*Password*</span></span> |  | <span data-ttu-id="0c433-143">Ustaw silne hasło do konta administratora.</span><span class="sxs-lookup"><span data-stu-id="0c433-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="0c433-144">*Potwierdź hasło*</span><span class="sxs-lookup"><span data-stu-id="0c433-144">*Confirm password*</span></span> |  | <span data-ttu-id="0c433-145">Potwierdź hasło konta administratora hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="0c433-146">*Lokalizacja*</span><span class="sxs-lookup"><span data-stu-id="0c433-146">*Location*</span></span> |  | <span data-ttu-id="0c433-147">Wybierz dostępny region.</span><span class="sxs-lookup"><span data-stu-id="0c433-147">Select an available region.</span></span> |
| <span data-ttu-id="0c433-148">*Wersja*</span><span class="sxs-lookup"><span data-stu-id="0c433-148">*Version*</span></span> | <span data-ttu-id="0c433-149">5.7</span><span class="sxs-lookup"><span data-stu-id="0c433-149">5.7</span></span> | <span data-ttu-id="0c433-150">Wybierz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="0c433-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="0c433-151">*Konfigurowanie wydajności*</span><span class="sxs-lookup"><span data-stu-id="0c433-151">*Configure performance*</span></span> | <span data-ttu-id="0c433-152">Podstawowe, 50 obliczeniowe jednostki, 50 GB</span><span class="sxs-lookup"><span data-stu-id="0c433-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="0c433-153">Wybierz pozycje **Warstwa cenowa**, **Jednostki obliczeniowe** i **Magazyn (GB)**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c433-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="0c433-154">*TooDashboard numeru PIN*</span><span class="sxs-lookup"><span data-stu-id="0c433-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="0c433-155">Zaznacz</span><span class="sxs-lookup"><span data-stu-id="0c433-155">Check</span></span> | <span data-ttu-id="0c433-156">Zalecane toocheck to pole, więc może zajść łatwo później na powitania serwera</span><span class="sxs-lookup"><span data-stu-id="0c433-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="0c433-157">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0c433-157">Then, click **Create**.</span></span> <span data-ttu-id="0c433-158">Minucie lub dwóch nowej bazy danych Azure MySQL serwera jest uruchomiona w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="0c433-159">Możesz kliknąć **powiadomienia** przycisk na proces wdrażania hello hello narzędzi toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0c433-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="0c433-160">Konfigurowanie zapory</span><span class="sxs-lookup"><span data-stu-id="0c433-160">Configure firewall</span></span>
<span data-ttu-id="0c433-161">Azure bazy danych dla programu MySQL są chronione przez zaporę.</span><span class="sxs-lookup"><span data-stu-id="0c433-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="0c433-162">Domyślnie wszystkie połączenia toohello serwera i hello bazy danych wewnątrz powitania serwera są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="0c433-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="0c433-163">Przed utworzeniem połączenia tooAzure bazy danych MySQL na powitania po raz pierwszy, skonfiguruj adres IP w sieci publicznej hello zapory tooadd powitania klienta na komputerze (lub zakres adresów IP).</span><span class="sxs-lookup"><span data-stu-id="0c433-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="0c433-164">Kliknij nowo utworzonego serwera, a następnie kliknij przycisk **zabezpieczenia połączeń**.</span><span class="sxs-lookup"><span data-stu-id="0c433-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="0c433-165">![Zabezpieczenia połączeń 3-1](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="0c433-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="0c433-166">Możesz **dodać Moje IP**, lub skonfigurować reguły zapory w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="0c433-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="0c433-167">Należy pamiętać, tooclick **zapisać** po utworzeniu reguły hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="0c433-168">Teraz możesz połączyć toohello serwera za pomocą narzędzia wiersza polecenia mysql lub MySQL Workbench graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0c433-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="0c433-169">Azure bazy danych MySQL serwera komunikuje się za pośrednictwem portu 3306.</span><span class="sxs-lookup"><span data-stu-id="0c433-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="0c433-170">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 3306 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="0c433-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0c433-171">Jeśli tak, nie można połączyć serwer MySQL tooAzure, chyba że dział IT otwiera port 3306.</span><span class="sxs-lookup"><span data-stu-id="0c433-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0c433-172">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="0c433-172">Get connection information</span></span>
<span data-ttu-id="0c433-173">W pełni kwalifikowana hello GET **nazwy serwera** i **nazwę logowania administratora serwera** bazy danych Azure, aby serwer MySQL z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0c433-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="0c433-174">Możesz użyć hello pełną nazwę tooconnect tooyour serwera za pomocą narzędzia wiersza polecenia mysql.</span><span class="sxs-lookup"><span data-stu-id="0c433-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="0c433-175">W [portalu Azure](https://portal.azure.com/), kliknij przycisk **wszystkie zasoby** z menu po lewej stronie powitania, nazwa typu hello i wyszukaj bazy danych Azure, aby serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="0c433-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="0c433-176">Wybierz hello — szczegóły hello tooview nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="0c433-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="0c433-177">W obszarze hello ustawienia kliknij pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0c433-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="0c433-178">Należy zanotować **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="0c433-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="0c433-179">Możesz kliknąć pozycję hello Kopiuj przycisku Dalej tooeach pola toocopy toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="0c433-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="0c433-180">![właściwości serwera 4-2](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="0c433-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="0c433-181">W tym przykładzie nazwa serwera hello jest *myserver4demo.mysql.database.azure.com*, i jest identyfikator logowania administratora serwera hello  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="0c433-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="0c433-182">Połącz serwer toohello przy użyciu mysql</span><span class="sxs-lookup"><span data-stu-id="0c433-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="0c433-183">Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour połączenia bazy danych platformy Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="0c433-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="0c433-184">Z hello powłoki chmury Azure w przeglądarce hello lub własnego komputera przy użyciu narzędzia mysql zainstalowane lokalnie, można uruchomić narzędzie wiersza polecenia hello mysql.</span><span class="sxs-lookup"><span data-stu-id="0c433-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="0c433-185">toolaunch hello powłoki chmury Azure, kliknij przycisk hello `Try It` przycisk blokiem kodu w tym artykule, lub odwiedź hello portalu Azure i kliknij przycisk hello `>_` ikonę w górnym prawym narzędzi hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="0c433-186">Wpisz tooconnect polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0c433-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="0c433-187">Tworzenie pustej bazy danych</span><span class="sxs-lookup"><span data-stu-id="0c433-187">Create a blank database</span></span>
<span data-ttu-id="0c433-188">Po wyświetleniu serwera połączonych toohello utworzyć toowork pustą bazę danych, z.</span><span class="sxs-lookup"><span data-stu-id="0c433-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="0c433-189">W wierszu hello Uruchom hello następujące polecenia tooswitch połączenia toothis nowo utworzone w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="0c433-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="0c433-190">Tworzenie tabel w bazie danych hello</span><span class="sxs-lookup"><span data-stu-id="0c433-190">Create tables in hello database</span></span>
<span data-ttu-id="0c433-191">Teraz, gdy wiesz, jak tooconnect toohello Azure bazy danych dla bazy danych MySQL, firma Microsoft może przejść przez jak toocomplete niektóre podstawowe zadania.</span><span class="sxs-lookup"><span data-stu-id="0c433-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="0c433-192">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="0c433-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="0c433-193">Teraz utworzyć tabelę, która przechowuje informacje dotyczące spisu.</span><span class="sxs-lookup"><span data-stu-id="0c433-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="0c433-194">Ładowanie danych do tabel hello</span><span class="sxs-lookup"><span data-stu-id="0c433-194">Load data into hello tables</span></span>
<span data-ttu-id="0c433-195">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="0c433-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="0c433-196">W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="0c433-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="0c433-197">Masz teraz dwa wiersze przykładowych danych do tabeli hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0c433-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="0c433-198">Zapytania i Aktualizuj hello dane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="0c433-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="0c433-199">Wykonanie poniższych informacji tooretrieve zapytania z tabeli bazy danych hello hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="0c433-200">Należy również zaktualizować hello dane w tabelach hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="0c433-201">wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="0c433-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="0c433-202">Przywracanie bazy danych tooa poprzedniego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="0c433-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="0c433-203">Wyobraź sobie przypadkowo usunięto tabelę ważne bazy danych i nie można łatwo odzyskać hello danych.</span><span class="sxs-lookup"><span data-stu-id="0c433-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="0c433-204">Bazy danych platformy Azure dla programu MySQL pozwala toorestore powitania serwera tooa punktu w czasie, tworząc kopię hello baz danych do nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="0c433-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="0c433-205">Można użyć tego nowego serwera toorecover usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="0c433-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="0c433-206">Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="0c433-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="0c433-207">W portalu Azure hello Znajdź bazy danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="0c433-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="0c433-208">Na powitania **omówienie** kliknij przycisk **przywrócić** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="0c433-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="0c433-209">zostanie otwarta strona przywracania Hello.</span><span class="sxs-lookup"><span data-stu-id="0c433-209">hello Restore page opens.</span></span>

   ![10-1 przywracania bazy danych](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="0c433-211">Wypełnianie hello **przywrócić** formularza hello wymagane informacje.</span><span class="sxs-lookup"><span data-stu-id="0c433-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![Formularz przywracania 10-2](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="0c433-213">**Punkt przywracania**: Wybierz w momencie, które mają toorestore, w czasie hello na liście.</span><span class="sxs-lookup"><span data-stu-id="0c433-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="0c433-214">Upewnij się, że tooconvert tooUTC Twojego lokalną strefę czasową.</span><span class="sxs-lookup"><span data-stu-id="0c433-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="0c433-215">**Przywracanie serwera toonew**: Podaj nową nazwę serwera ma toorestore do.</span><span class="sxs-lookup"><span data-stu-id="0c433-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="0c433-216">**Lokalizacja**: hello region jest taki sam jak powitania serwera źródłowego i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="0c433-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="0c433-217">**Warstwa cenowa**: hello warstwa cenowa jest hello identyczny powitania serwera źródłowego i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="0c433-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="0c433-218">Kliknij przycisk **OK** toorestore hello serwera zbyt[tooa punktu przywracania w czasie](./howto-restore-server-portal.md) przed hello tabeli został usunięty.</span><span class="sxs-lookup"><span data-stu-id="0c433-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="0c433-219">Przywracanie serwera tworzy nową kopię powitania serwera, począwszy od hello punktu w czasie, które określisz.</span><span class="sxs-lookup"><span data-stu-id="0c433-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c433-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c433-220">Next steps</span></span>
<span data-ttu-id="0c433-221">W tym samouczku użyjesz hello toolearned portalu Azure, jak do:</span><span class="sxs-lookup"><span data-stu-id="0c433-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0c433-222">Utwórz bazę danych systemu Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="0c433-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="0c433-223">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="0c433-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="0c433-224">Użyj mysql narzędzia wiersza polecenia toocreate bazy danych</span><span class="sxs-lookup"><span data-stu-id="0c433-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="0c433-225">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="0c433-225">Load sample data</span></span>
> * <span data-ttu-id="0c433-226">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="0c433-226">Query data</span></span>
> * <span data-ttu-id="0c433-227">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="0c433-227">Update data</span></span>
> * <span data-ttu-id="0c433-228">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="0c433-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c433-229">Jak tooconnect tooAzure aplikacji bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="0c433-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
