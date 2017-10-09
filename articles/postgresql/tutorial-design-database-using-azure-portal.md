---
title: "Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak tooDesign Twojego pierwszego Azure bazy danych PostgreSQL przy użyciu hello portalu Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: fde7e9d1ae2bad4291d18bebd3356f4f8a2ac86a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="87d7c-103">Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="87d7c-103">Design your first Azure Database for PostgreSQL using hello Azure portal</span></span>

<span data-ttu-id="87d7c-104">Bazy danych platformy Azure dla PostgreSQL jest zarządzana usługa, która pozwala toorun, zarządzanie i skalowania wysokiej dostępności PostgreSQL baz danych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="87d7c-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="87d7c-105">Przy użyciu hello portalu Azure, można łatwo zarządzać serwerem i projektowanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="87d7c-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="87d7c-106">W tym samouczku użyjesz hello toolearn portalu Azure, jak do:</span><span class="sxs-lookup"><span data-stu-id="87d7c-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="87d7c-107">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="87d7c-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="87d7c-108">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="87d7c-109">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate Narzędzia bazy danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="87d7c-110">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="87d7c-110">Load sample data</span></span>
> * <span data-ttu-id="87d7c-111">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="87d7c-111">Query data</span></span>
> * <span data-ttu-id="87d7c-112">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-112">Update data</span></span>
> * <span data-ttu-id="87d7c-113">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87d7c-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="87d7c-114">Prerequisites</span></span>
<span data-ttu-id="87d7c-115">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="87d7c-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="87d7c-116">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="87d7c-116">Log in toohello Azure portal</span></span>
<span data-ttu-id="87d7c-117">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87d7c-117">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="87d7c-118">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="87d7c-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="87d7c-119">Serwer usługi Azure Database for PostgreSQL jest tworzony ze zdefiniowanym zestawem [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="87d7c-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="87d7c-120">Serwer Hello jest tworzony w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87d7c-120">hello server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="87d7c-121">Wykonaj te kroki toocreate bazy danych Azure PostgreSQL serwera:</span><span class="sxs-lookup"><span data-stu-id="87d7c-121">Follow these steps toocreate an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="87d7c-122">Kliknij przycisk hello **+ nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="87d7c-122">Click hello **+ New**  button found on hello upper left-hand corner of hello Azure portal.</span></span>
2.  <span data-ttu-id="87d7c-123">Wybierz **baz danych** z hello **nowy** i wybrać opcję **bazą danych Azure dla PostgreSQL** z hello **baz danych** strony.</span><span class="sxs-lookup"><span data-stu-id="87d7c-123">Select **Databases** from hello **New** page, and select **Azure Database for PostgreSQL** from hello **Databases** page.</span></span>
 <span data-ttu-id="87d7c-124">![Bazy danych platformy Azure dla PostgreSQL — tworzenie hello bazy danych](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="87d7c-124">![Azure Database for PostgreSQL - Create hello database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="87d7c-125">Wypełnianie hello nowego serwera szczegóły formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:</span><span class="sxs-lookup"><span data-stu-id="87d7c-125">Fill out hello new server details form with hello following information, as shown on hello preceding image:</span></span>
    - <span data-ttu-id="87d7c-126">Nazwa serwera: **mypgserver 20170401** (nazwa serwera mapuje nazwę tooDNS i w związku z tym jest wymagana toobe globalnie unikatowy)</span><span class="sxs-lookup"><span data-stu-id="87d7c-126">Server name: **mypgserver-20170401** (name of a server maps tooDNS name and is thus required toobe globally unique)</span></span> 
    - <span data-ttu-id="87d7c-127">Subskrypcja: Jeśli masz wiele subskrypcji, wybierz hello odpowiednie subskrypcji, w którym hello zasobów istnieje lub jest on rozliczany dla.</span><span class="sxs-lookup"><span data-stu-id="87d7c-127">Subscription: If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span>
    - <span data-ttu-id="87d7c-128">Grupa zasobów: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="87d7c-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="87d7c-129">Wybrane przez Ciebie login i hasło administratora serwera</span><span class="sxs-lookup"><span data-stu-id="87d7c-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="87d7c-130">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="87d7c-130">Location</span></span>
    - <span data-ttu-id="87d7c-131">Wersja PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="87d7c-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="87d7c-132">Hello identyfikator logowania administratora serwera i hasło, które są określone w tym miejscu są wymagane toolog Server toohello i jej baz danych w dalszej części tego szybki start.</span><span class="sxs-lookup"><span data-stu-id="87d7c-132">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="87d7c-133">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="87d7c-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="87d7c-134">Kliknij przycisk **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="87d7c-134">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="87d7c-135">W tym przewodniku Szybki start wybierz warstwę **Podstawowa**, **50 jednostek obliczeniowych** i **50 GB** dołączonej pamięci.</span><span class="sxs-lookup"><span data-stu-id="87d7c-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="87d7c-136">![Bazy danych platformy Azure dla PostgreSQL — warstwy usług hello pobrania](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="87d7c-136">![Azure Database for PostgreSQL - pick hello service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="87d7c-137">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="87d7c-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="87d7c-138">Kliknij przycisk **Utwórz** tooprovision powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="87d7c-138">Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="87d7c-139">Aprowizacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="87d7c-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="87d7c-140">Sprawdź hello **toodashboard numeru Pin** opcji tooallow łatwe monitorowanie wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="87d7c-140">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="87d7c-141">Na pasku narzędzi hello, kliknij przycisk **powiadomienia** procesu wdrażania hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="87d7c-141">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>
 <span data-ttu-id="87d7c-142">![Usługa Azure Database for PostgreSQL — patrz Powiadomienia](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="87d7c-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="87d7c-143">Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze.</span><span class="sxs-lookup"><span data-stu-id="87d7c-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="87d7c-144">Witaj [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) baza danych jest domyślna baza danych przeznaczone do użytku przez użytkowników, narzędzia i aplikacje innych producentów.</span><span class="sxs-lookup"><span data-stu-id="87d7c-144">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="87d7c-145">Konfigurowanie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="87d7c-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="87d7c-146">Hello Azure bazy danych dla usługi PostgreSQL tworzy zapory na poziomie serwera hello.</span><span class="sxs-lookup"><span data-stu-id="87d7c-146">hello Azure Database for PostgreSQL service creates a firewall at hello server-level.</span></span> <span data-ttu-id="87d7c-147">Zapora uniemożliwia aplikacji zewnętrznych i narzędzia łączenia serwera toohello i żadnych baz danych na serwerze hello, chyba że tooopen hello zapory dla określonych adresów IP jest tworzona reguła zapory.</span><span class="sxs-lookup"><span data-stu-id="87d7c-147">This firewall prevents external applications and tools from connecting toohello server and any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="87d7c-148">Po zakończeniu wdrażania hello, kliknij przycisk **wszystkie zasoby** z menu po lewej stronie powitania i wpisz nazwę hello **mypgserver 20170401** toosearch dla nowo utworzonego serwera.</span><span class="sxs-lookup"><span data-stu-id="87d7c-148">After hello deployment completes, click **All Resources** from hello left-hand menu and type in hello name **mypgserver-20170401** toosearch for your newly created server.</span></span> <span data-ttu-id="87d7c-149">Kliknij nazwę serwera hello hello wynik wyszukiwania na liście.</span><span class="sxs-lookup"><span data-stu-id="87d7c-149">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="87d7c-150">Witaj **omówienie** strony dla serwera zostanie otwarty i udostępnia opcje dla dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="87d7c-150">hello **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="87d7c-151">Azure Database for PostgreSQL — wyszukiwanie serwera</span><span class="sxs-lookup"><span data-stu-id="87d7c-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="87d7c-152">W bloku serwera hello, wybierz **zabezpieczenia połączeń**.</span><span class="sxs-lookup"><span data-stu-id="87d7c-152">In hello server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="87d7c-153">Kliknij w polu tekstowym hello w obszarze **Nazwa reguły** i dodać nowe zapory reguły toowhitelist hello zakres adresów IP w łączności.</span><span class="sxs-lookup"><span data-stu-id="87d7c-153">Click in hello text box under **Rule Name,** and add a new firewall rule toowhitelist hello IP range for connectivity.</span></span> <span data-ttu-id="87d7c-154">W tym samouczku umożliwia Zezwalaj na wszystkie adresy IP, wpisując w **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** i **końcowemu adresowi IP = 255.255.255.255** , a następnie kliknij przycisk **Zapisz** .</span><span class="sxs-lookup"><span data-stu-id="87d7c-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="87d7c-155">Można ustawić reguły zapory, która obejmuje IP zakresu toobe stanie tooconnect z sieci.</span><span class="sxs-lookup"><span data-stu-id="87d7c-155">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span>
 
 ![Usługa Azure Database for PostgreSQL — tworzenie reguły zapory](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="87d7c-157">Kliknij przycisk **zapisać** , a następnie kliknij przycisk hello **X** tooclose hello **zabezpieczenia połączeń** strony.</span><span class="sxs-lookup"><span data-stu-id="87d7c-157">Click **Save** and then click hello **X** tooclose hello **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="87d7c-158">Serwer Azure PostgreSQL komunikuje się przez port 5432.</span><span class="sxs-lookup"><span data-stu-id="87d7c-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="87d7c-159">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 5432 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="87d7c-159">If you are trying tooconnect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="87d7c-160">Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 5432.</span><span class="sxs-lookup"><span data-stu-id="87d7c-160">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-hello-connection-information"></a><span data-ttu-id="87d7c-161">Pobierz informacje o połączeniu hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-161">Get hello connection information</span></span>

<span data-ttu-id="87d7c-162">Tworząc naszej bazie danych Azure dla serwera PostgreSQL, hello domyślne **postgres** bazy danych również pobiera utworzony.</span><span class="sxs-lookup"><span data-stu-id="87d7c-162">When we created our Azure Database for PostgreSQL server, hello default **postgres** database also gets created.</span></span> <span data-ttu-id="87d7c-163">tooconnect tooyour serwera bazy danych, należy tooprovide hosta dostępu i informacji o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="87d7c-163">tooconnect tooyour database server, you need tooprovide host information and access credentials.</span></span>

1. <span data-ttu-id="87d7c-164">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj serwera hello właśnie utworzony **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="87d7c-164">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="87d7c-165">Azure Database for PostgreSQL — wyszukiwanie serwera</span><span class="sxs-lookup"><span data-stu-id="87d7c-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="87d7c-166">Kliknij nazwę serwera hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="87d7c-166">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="87d7c-167">Wybierz powitania serwera **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="87d7c-167">Select hello server's **Overview** page.</span></span> <span data-ttu-id="87d7c-168">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="87d7c-168">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="87d7c-170">Połącz tooPostgreSQL bazy danych przy użyciu psql w powłoce chmury</span><span class="sxs-lookup"><span data-stu-id="87d7c-170">Connect tooPostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="87d7c-171">Użyjmy teraz hello psql narzędzia wiersza polecenia tooconnect toohello bazy danych Azure, PostgreSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="87d7c-171">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="87d7c-172">Uruchom program hello powłoki chmury Azure za pomocą ikony terminali hello w okienku nawigacji w górnym hello.</span><span class="sxs-lookup"><span data-stu-id="87d7c-172">Launch hello Azure Cloud Shell via hello terminal icon on hello top navigation pane.</span></span>

   ![Azure Database for PostgreSQL — ikona terminala powłoki Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="87d7c-174">Witaj powłoki chmury Azure otwiera w przeglądarce, umożliwiając tootype bash polecenia.</span><span class="sxs-lookup"><span data-stu-id="87d7c-174">hello Azure Cloud Shell opens in your browser, enabling you tootype bash commands.</span></span>

   ![Azure Database for PostgreSQL — znak zachęty powłoki Azure Shell Bash](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="87d7c-176">W wierszu polecenia powłoki chmury hello połączyć tooyour bazy danych Azure za pomocą poleceń psql powitania serwera PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="87d7c-176">At hello Cloud Shell prompt, connect tooyour Azure Database for PostgreSQL server using hello psql commands.</span></span> <span data-ttu-id="87d7c-177">Witaj następujący format jest używane tooconnect tooan Azure bazy danych dla serwera PostgreSQL z hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie:</span><span class="sxs-lookup"><span data-stu-id="87d7c-177">hello following format is used tooconnect tooan Azure Database for PostgreSQL server with hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="87d7c-178">Na przykład następujące polecenie hello łączy toohello domyślna baza danych o nazwie **postgres** na serwerze PostgreSQL **mypgserver 20170401.postgres.database.azure.com** przy użyciu poświadczeń dostępu.</span><span class="sxs-lookup"><span data-stu-id="87d7c-178">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="87d7c-179">Po wyświetleniu monitu wprowadź hasło administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="87d7c-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="87d7c-180">Utwórz nową bazę danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-180">Create a New Database</span></span>
<span data-ttu-id="87d7c-181">Po wyświetleniu toohello połączony serwer Utwórz pustą bazę danych w wierszu hello.</span><span class="sxs-lookup"><span data-stu-id="87d7c-181">Once you're connected toohello server, create a blank database at hello prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="87d7c-182">W wierszu polecenia hello wykonania hello następujące polecenia tooswitch połączenia toohello nowo utworzone w bazie danych **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="87d7c-182">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-hello-database"></a><span data-ttu-id="87d7c-183">Tworzenie tabel w bazie danych hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-183">Create tables in hello database</span></span>
<span data-ttu-id="87d7c-184">Teraz, gdy wiesz, jak toohello tooconnect bazą danych Azure dla PostgreSQL, firma Microsoft może przejść w sposób toocomplete niektóre podstawowe zadania.</span><span class="sxs-lookup"><span data-stu-id="87d7c-184">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="87d7c-185">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="87d7c-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="87d7c-186">Ta funkcja pozwala utworzyć tabelę, która śledzi informacje o spisie.</span><span class="sxs-lookup"><span data-stu-id="87d7c-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="87d7c-187">Można wyświetlić hello nowo utworzona tabela hello liście tabvles teraz, wpisując:</span><span class="sxs-lookup"><span data-stu-id="87d7c-187">You can see hello newly created table in hello list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="87d7c-188">Ładowanie danych do tabel hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-188">Load data into hello tables</span></span>
<span data-ttu-id="87d7c-189">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="87d7c-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="87d7c-190">W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-190">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="87d7c-191">Masz teraz dwa wiersze przykładowych danych do tabeli hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="87d7c-191">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="87d7c-192">Zapytania i Aktualizuj hello dane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-192">Query and update hello data in hello tables</span></span>
<span data-ttu-id="87d7c-193">Wykonanie poniższych informacji tooretrieve zapytania z tabeli bazy danych hello hello.</span><span class="sxs-lookup"><span data-stu-id="87d7c-193">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="87d7c-194">Można także zaktualizować hello dane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-194">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="87d7c-195">wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="87d7c-195">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-tooa-previous-point-in-time"></a><span data-ttu-id="87d7c-196">Przywracanie danych tooa wcześniejszego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="87d7c-196">Restore data tooa previous point in time</span></span>
<span data-ttu-id="87d7c-197">Załóżmy, że zostanie przypadkowo usunięte w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="87d7c-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="87d7c-198">Ta sytuacja jest coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="87d7c-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="87d7c-199">Bazy danych platformy Azure dla PostgreSQL umożliwia toogo tooany Wstecz w momencie (w hello ostatnich dni too7 (Basic) i 35 dni (standardowe)) i przywracania w momencie tooa nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="87d7c-199">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="87d7c-200">Można użyć tego nowego serwera toorecover usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="87d7c-200">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="87d7c-201">Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="87d7c-201">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1.  <span data-ttu-id="87d7c-202">Na hello Azure bazy danych PostgreSQL strony serwera, kliknij przycisk **przywrócić** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="87d7c-202">On hello Azure Database for PostgreSQL page for your server, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="87d7c-203">Witaj **przywrócić** zostanie otwarta strona.</span><span class="sxs-lookup"><span data-stu-id="87d7c-203">hello **Restore** page opens.</span></span>
  <span data-ttu-id="87d7c-204">![Portal Azure — opcje przywracania formularza](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="87d7c-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="87d7c-205">Wypełnianie hello **przywrócić** formularza hello wymagane informacje:</span><span class="sxs-lookup"><span data-stu-id="87d7c-205">Fill out hello **Restore** form with hello required information:</span></span>

  ![Portal Azure — opcje przywracania formularza](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="87d7c-207">**Punkt przywracania**: Wybierz w momencie po hello serwer został zmieniony</span><span class="sxs-lookup"><span data-stu-id="87d7c-207">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="87d7c-208">**Serwer docelowy**: Podaj nową nazwę serwera ma toorestore do</span><span class="sxs-lookup"><span data-stu-id="87d7c-208">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="87d7c-209">**Lokalizacja**: nie można wybrać hello region, domyślnie jest taka sama jak powitania serwera źródłowego</span><span class="sxs-lookup"><span data-stu-id="87d7c-209">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="87d7c-210">**Warstwa cenowa**: nie można zmienić tę wartość podczas przywracania serwera.</span><span class="sxs-lookup"><span data-stu-id="87d7c-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="87d7c-211">Jest taki sam jak powitania serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="87d7c-211">It is same as hello source server.</span></span> 
3.  <span data-ttu-id="87d7c-212">Kliknij przycisk **OK** toorestore hello serwera zbyt[tooa w momencie przywracania](./howto-restore-server-portal.md) przed tabel hello został usunięty.</span><span class="sxs-lookup"><span data-stu-id="87d7c-212">Click **OK** toorestore hello server too[restore tooa point-in-time](./howto-restore-server-portal.md) before hello tables was deleted.</span></span> <span data-ttu-id="87d7c-213">Przywracanie serwera tooa innego punktu w czasie tworzy zduplikowane nowy serwer jako hello oryginalny serwer określoną hello punktu w czasie, pod warunkiem, że w okresie przechowywania hello dla Twojego [warstwy usług](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="87d7c-213">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87d7c-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="87d7c-214">Next Steps</span></span>
<span data-ttu-id="87d7c-215">W tym samouczku przedstawiono sposób toouse hello portalu Azure i inne narzędzia do:</span><span class="sxs-lookup"><span data-stu-id="87d7c-215">In this tutorial, you learned how toouse hello Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="87d7c-216">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="87d7c-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="87d7c-217">Konfigurowanie zapory serwera hello</span><span class="sxs-lookup"><span data-stu-id="87d7c-217">Configure hello server firewall</span></span>
> * <span data-ttu-id="87d7c-218">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate Narzędzia bazy danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="87d7c-219">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="87d7c-219">Load sample data</span></span>
> * <span data-ttu-id="87d7c-220">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="87d7c-220">Query data</span></span>
> * <span data-ttu-id="87d7c-221">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-221">Update data</span></span>
> * <span data-ttu-id="87d7c-222">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="87d7c-222">Restore data</span></span>

<span data-ttu-id="87d7c-223">Następnie Dowiedz się, jak toouse interfejsu wiersza polecenia Azure toodo podobne zadania, przejrzyj tego samouczka: [projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="87d7c-223">Next, learn how toouse Azure CLI toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
