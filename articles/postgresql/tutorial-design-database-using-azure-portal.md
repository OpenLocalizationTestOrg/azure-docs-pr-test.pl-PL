---
title: "Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak projektować pod kątem PostgreSQL pierwszą bazę danych Azure przy użyciu portalu Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: 2aa9d10749b54537495ad3e09566c43718f67a9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="f22f8-103">Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f22f8-103">Design your first Azure Database for PostgreSQL using the Azure portal</span></span>

<span data-ttu-id="f22f8-104">Azure Database for PostgreSQL to usługa zarządzana, która umożliwia uruchamianie i skalowanie w chmurze baz danych PostgreSQL o wysokiej dostępności, a także zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="f22f8-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="f22f8-105">Przy użyciu portalu Azure, można łatwo zarządzać serwerem i projektowanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f22f8-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="f22f8-106">W tym samouczku, użyj portalu Azure Aby dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="f22f8-106">In this tutorial, you use the Azure portal to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f22f8-107">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f22f8-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="f22f8-108">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="f22f8-108">Configure the server firewall</span></span>
> * <span data-ttu-id="f22f8-109">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie do tworzenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="f22f8-110">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="f22f8-110">Load sample data</span></span>
> * <span data-ttu-id="f22f8-111">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="f22f8-111">Query data</span></span>
> * <span data-ttu-id="f22f8-112">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-112">Update data</span></span>
> * <span data-ttu-id="f22f8-113">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f22f8-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f22f8-114">Prerequisites</span></span>
<span data-ttu-id="f22f8-115">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="f22f8-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="f22f8-116">Logowanie do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f22f8-116">Log in to the Azure portal</span></span>
<span data-ttu-id="f22f8-117">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f22f8-117">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="f22f8-118">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f22f8-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="f22f8-119">Serwer usługi Azure Database for PostgreSQL jest tworzony ze zdefiniowanym zestawem [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="f22f8-120">Serwer jest tworzony w ramach [grupy zasobów Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-120">The server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f22f8-121">Wykonaj następujące kroki, aby utworzyć serwer usługi Azure Database for PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="f22f8-121">Follow these steps to create an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="f22f8-122">Kliknij przycisk **+ nowy** znaleziono przycisku w lewym górnym rogu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f22f8-122">Click the **+ New**  button found on the upper left-hand corner of the Azure portal.</span></span>
2.  <span data-ttu-id="f22f8-123">Na stronie **Nowy** wybierz pozycję **Bazy danych**, a następnie na stronie **Bazy danych** wybierz pozycję **Azure Database for PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-123">Select **Databases** from the **New** page, and select **Azure Database for PostgreSQL** from the **Databases** page.</span></span>
 <span data-ttu-id="f22f8-124">![Usługa Azure Database for PostgreSQL — tworzenie bazy danych](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="f22f8-124">![Azure Database for PostgreSQL - Create the database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="f22f8-125">Wypełnij formularz informacjami o szczegółach nowego serwera w sposób pokazany na wcześniejszej ilustracji, używając następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="f22f8-125">Fill out the new server details form with the following information, as shown on the preceding image:</span></span>
    - <span data-ttu-id="f22f8-126">Nazwa serwera: **mypgserver-20170401** (nazwa serwera jest mapowana na nazwę DNS i dlatego musi być globalnie unikatowa)</span><span class="sxs-lookup"><span data-stu-id="f22f8-126">Server name: **mypgserver-20170401** (name of a server maps to DNS name and is thus required to be globally unique)</span></span> 
    - <span data-ttu-id="f22f8-127">Subskrypcja: jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w ramach której istnieje zasób lub będą za niego naliczane opłaty.</span><span class="sxs-lookup"><span data-stu-id="f22f8-127">Subscription: If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span>
    - <span data-ttu-id="f22f8-128">Grupa zasobów: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="f22f8-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="f22f8-129">Wybrane przez Ciebie login i hasło administratora serwera</span><span class="sxs-lookup"><span data-stu-id="f22f8-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="f22f8-130">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="f22f8-130">Location</span></span>
    - <span data-ttu-id="f22f8-131">Wersja PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f22f8-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f22f8-132">Login i hasło administratora serwera określone w tym miejscu będą wymagane do logowania do serwera i jego baz danych w późniejszej części tego przewodnika Szybki start.</span><span class="sxs-lookup"><span data-stu-id="f22f8-132">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="f22f8-133">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="f22f8-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="f22f8-134">Kliknij pozycję **Warstwa cenowa**, aby określić warstwę usługi i poziom wydajności dla nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f22f8-134">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="f22f8-135">W tym przewodniku Szybki start wybierz warstwę **Podstawowa**, **50 jednostek obliczeniowych** i **50 GB** dołączonej pamięci.</span><span class="sxs-lookup"><span data-stu-id="f22f8-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="f22f8-136">![Usługa Azure Database for PostgreSQL — wybór warstwy usług](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="f22f8-136">![Azure Database for PostgreSQL - pick the service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="f22f8-137">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="f22f8-138">Kliknij przycisk **Utwórz**, aby aprowizować serwer.</span><span class="sxs-lookup"><span data-stu-id="f22f8-138">Click **Create** to provision the server.</span></span> <span data-ttu-id="f22f8-139">Aprowizacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f22f8-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="f22f8-140">Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, aby łatwo śledzić wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f22f8-140">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="f22f8-141">Na pasku narzędzi kliknij pozycję **Powiadomienia**, aby monitorować proces wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f22f8-141">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>
 <span data-ttu-id="f22f8-142">![Usługa Azure Database for PostgreSQL — patrz Powiadomienia](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="f22f8-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="f22f8-143">Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze.</span><span class="sxs-lookup"><span data-stu-id="f22f8-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="f22f8-144">Baza danych [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) to domyślna baza danych przeznaczona do użycia dla użytkowników oraz na potrzeby narzędzi i aplikacji innych firm.</span><span class="sxs-lookup"><span data-stu-id="f22f8-144">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="f22f8-145">Konfigurowanie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="f22f8-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="f22f8-146">Usługa Azure Database for PostgreSQL tworzy zaporę na poziomie serwera.</span><span class="sxs-lookup"><span data-stu-id="f22f8-146">The Azure Database for PostgreSQL service creates a firewall at the server-level.</span></span> <span data-ttu-id="f22f8-147">Ta zapora uniemożliwia zewnętrznym aplikacjom i narzędziom łączenie się z serwerem i wszelkimi bazami danych na tym serwerze, chyba że zostanie utworzona reguła zapory otwierająca zaporę dla konkretnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="f22f8-147">This firewall prevents external applications and tools from connecting to the server and any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="f22f8-148">Po zakończeniu wdrożenia kliknij pozycję **Wszystkie zasoby** w menu po lewej stronie i wpisz nazwę **mypgserver-20170401**, aby wyszukać nowo utworzony serwer.</span><span class="sxs-lookup"><span data-stu-id="f22f8-148">After the deployment completes, click **All Resources** from the left-hand menu and type in the name **mypgserver-20170401** to search for your newly created server.</span></span> <span data-ttu-id="f22f8-149">Kliknij nazwę serwera wyświetlaną w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f22f8-149">Click the server name listed in the search result.</span></span> <span data-ttu-id="f22f8-150">Zostanie otwarta strona **Przegląd**, która zawiera dalsze opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f22f8-150">The **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="f22f8-151">Azure Database for PostgreSQL — wyszukiwanie serwera</span><span class="sxs-lookup"><span data-stu-id="f22f8-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="f22f8-152">W bloku serwera wybierz opcję **Zabezpieczenia połączeń**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-152">In the server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="f22f8-153">Kliknij w polu tekstowym w obszarze **Nazwa reguły** i dodaj nową regułę zapory, aby na liście dozwolonych umieścić zakres adresów IP służących do łączności.</span><span class="sxs-lookup"><span data-stu-id="f22f8-153">Click in the text box under **Rule Name,** and add a new firewall rule to whitelist the IP range for connectivity.</span></span> <span data-ttu-id="f22f8-154">W tym samouczku umożliwia Zezwalaj na wszystkie adresy IP, wpisując w **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** i **końcowemu adresowi IP = 255.255.255.255** , a następnie kliknij przycisk **Zapisz** .</span><span class="sxs-lookup"><span data-stu-id="f22f8-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="f22f8-155">Możesz ustawić regułę zapory uwzględniającą zakres adresów IP, aby mieć możliwość nawiązywania połączeń z Twojej sieci.</span><span class="sxs-lookup"><span data-stu-id="f22f8-155">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span>
 
 ![Usługa Azure Database for PostgreSQL — tworzenie reguły zapory](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="f22f8-157">Kliknij przycisk **Zapisz**, a następnie kliknij przycisk **X**, aby zamknąć stronę **Zabezpieczenia połączeń**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-157">Click **Save** and then click the **X** to close the **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f22f8-158">Serwer Azure PostgreSQL komunikuje się przez port 5432.</span><span class="sxs-lookup"><span data-stu-id="f22f8-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="f22f8-159">Jeśli próbujesz nawiązać połączenie z sieci firmowej, ruch wychodzący na porcie 5432 może być zablokowany przez zaporę sieciową.</span><span class="sxs-lookup"><span data-stu-id="f22f8-159">If you are trying to connect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="f22f8-160">Jeśli zachodzi taka sytuacja, nie będzie można nawiązać połączenia z serwerem usługi Azure SQL Database, chyba że dział IT otworzy port 5432.</span><span class="sxs-lookup"><span data-stu-id="f22f8-160">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-the-connection-information"></a><span data-ttu-id="f22f8-161">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="f22f8-161">Get the connection information</span></span>

<span data-ttu-id="f22f8-162">Podczas tworzenia serwera usługi Azure Database for PostgreSQL, domyślnie jest także tworzona baza danych **postgres**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-162">When we created our Azure Database for PostgreSQL server, the default **postgres** database also gets created.</span></span> <span data-ttu-id="f22f8-163">Aby nawiązać połączenie z serwerem bazy danych, musisz podać informacje o hoście i poświadczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="f22f8-163">To connect to your database server, you need to provide host information and access credentials.</span></span>

1. <span data-ttu-id="f22f8-164">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj właśnie utworzony serwer **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-164">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="f22f8-165">Azure Database for PostgreSQL — wyszukiwanie serwera</span><span class="sxs-lookup"><span data-stu-id="f22f8-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="f22f8-166">Kliknij nazwę serwera **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-166">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="f22f8-167">Wybierz stronę serwera **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-167">Select the server's **Overview** page.</span></span> <span data-ttu-id="f22f8-168">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-168">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-to-postgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="f22f8-170">Nawiązywanie połączenia z bazą danych PostgreSQL w powłoce Cloud Shell za pomocą narzędzia psql</span><span class="sxs-lookup"><span data-stu-id="f22f8-170">Connect to PostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="f22f8-171">Użyj teraz narzędzia wiersza polecenia psql, aby nawiązać połączenie z serwerem usługi Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f22f8-171">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="f22f8-172">Uruchom powłokę Azure Cloud Shell za pośrednictwem ikony terminala w górnym okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="f22f8-172">Launch the Azure Cloud Shell via the terminal icon on the top navigation pane.</span></span>

   ![Azure Database for PostgreSQL — ikona terminala powłoki Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="f22f8-174">Powłoka Azure Cloud Shell zostanie otwarta w przeglądarce, umożliwiając wpisywanie poleceń powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="f22f8-174">The Azure Cloud Shell opens in your browser, enabling you to type bash commands.</span></span>

   ![Azure Database for PostgreSQL — znak zachęty powłoki Azure Shell Bash](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="f22f8-176">W wierszu polecenia powłoki Cloud Shell nawiąż połączenie z serwerem usługi Azure Database for PostgreSQL za pomocą poleceń psql.</span><span class="sxs-lookup"><span data-stu-id="f22f8-176">At the Cloud Shell prompt, connect to your Azure Database for PostgreSQL server using the psql commands.</span></span> <span data-ttu-id="f22f8-177">Następujący format służy do łączenia z serwerem usługi Azure Database for PostgreSQL przy użyciu narzędzia [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html):</span><span class="sxs-lookup"><span data-stu-id="f22f8-177">The following format is used to connect to an Azure Database for PostgreSQL server with the [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="f22f8-178">Na przykład poniższe polecenie nawiązuje połączenie z domyślną bazą danych o nazwie **postgres** na Twoim serwerze PostgreSQL **mypgserver-20170401.postgres.database.azure.com** za pomocą poświadczeń dostępu.</span><span class="sxs-lookup"><span data-stu-id="f22f8-178">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="f22f8-179">Po wyświetleniu monitu wprowadź hasło administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="f22f8-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="f22f8-180">Utwórz nową bazę danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-180">Create a New Database</span></span>
<span data-ttu-id="f22f8-181">Po nawiązaniu połączenia z serwerem utwórz pustą bazę danych za pomocą wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f22f8-181">Once you're connected to the server, create a blank database at the prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="f22f8-182">W wierszu polecenia wykonaj poniższe polecenie, aby przełączyć połączenie na nowo utworzoną bazę danych **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="f22f8-182">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-the-database"></a><span data-ttu-id="f22f8-183">Tworzenie tabel w bazie danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-183">Create tables in the database</span></span>
<span data-ttu-id="f22f8-184">Teraz, Znając sposób nawiązywania połączenia z bazą danych Azure dla PostgreSQL możemy przekazywane sposób wykonania zadania podstawowe.</span><span class="sxs-lookup"><span data-stu-id="f22f8-184">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="f22f8-185">Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="f22f8-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="f22f8-186">Ta funkcja pozwala utworzyć tabelę, która śledzi informacje o spisie.</span><span class="sxs-lookup"><span data-stu-id="f22f8-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="f22f8-187">Nowo utworzona tabela na liście tabvles można teraz wyświetlić, wpisując:</span><span class="sxs-lookup"><span data-stu-id="f22f8-187">You can see the newly created table in the list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="f22f8-188">Ładowanie danych do tabel</span><span class="sxs-lookup"><span data-stu-id="f22f8-188">Load data into the tables</span></span>
<span data-ttu-id="f22f8-189">Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego.</span><span class="sxs-lookup"><span data-stu-id="f22f8-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="f22f8-190">W oknie Otwórz okno wiersza polecenia Uruchom następujące zapytanie do wstawienia niektórych wierszy danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-190">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="f22f8-191">Masz teraz dwa wiersze przykładowych danych do tabeli utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="f22f8-191">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="f22f8-192">Zapytania i zaktualizować dane w tabelach</span><span class="sxs-lookup"><span data-stu-id="f22f8-192">Query and update the data in the tables</span></span>
<span data-ttu-id="f22f8-193">Wykonaj następujące zapytanie, aby pobrać informacje z tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f22f8-193">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="f22f8-194">Możesz również zaktualizować dane w tabelach</span><span class="sxs-lookup"><span data-stu-id="f22f8-194">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="f22f8-195">Wiersz jest odpowiednio aktualizowany podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="f22f8-195">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-to-a-previous-point-in-time"></a><span data-ttu-id="f22f8-196">Przywróć dane z wcześniejszego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="f22f8-196">Restore data to a previous point in time</span></span>
<span data-ttu-id="f22f8-197">Załóżmy, że zostanie przypadkowo usunięte w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f22f8-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="f22f8-198">Ta sytuacja jest coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="f22f8-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="f22f8-199">Bazy danych platformy Azure dla PostgreSQL umożliwia wróć do dowolnego punktu na czas (w ostatnim maksymalnie 7 dni (Basic), a 35 dni (standardowe)) i przywrócić tego punktu w czasie na nowy serwer.</span><span class="sxs-lookup"><span data-stu-id="f22f8-199">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="f22f8-200">Możesz użyć tego nowego serwera, aby odzyskać usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="f22f8-200">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="f22f8-201">Poniższe kroki należy przywrócić działanie serwera próbki do punktu przed tabeli został dodany.</span><span class="sxs-lookup"><span data-stu-id="f22f8-201">The following steps restore the sample server to a point before the table was added.</span></span>

1.  <span data-ttu-id="f22f8-202">W bazie danych Azure PostgreSQL strony serwera, kliknij przycisk **przywrócić** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="f22f8-202">On the Azure Database for PostgreSQL page for your server, click **Restore** on the toolbar.</span></span> <span data-ttu-id="f22f8-203">**Przywrócić** zostanie otwarta strona.</span><span class="sxs-lookup"><span data-stu-id="f22f8-203">The **Restore** page opens.</span></span>
  <span data-ttu-id="f22f8-204">![Portal Azure — opcje przywracania formularza](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="f22f8-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="f22f8-205">Wypełnianie **przywrócić** formularza z informacjami wymaganymi:</span><span class="sxs-lookup"><span data-stu-id="f22f8-205">Fill out the **Restore** form with the required information:</span></span>

  ![Portal Azure — opcje przywracania formularza](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="f22f8-207">**Punkt przywracania**: Wybierz w momencie po serwer został zmieniony</span><span class="sxs-lookup"><span data-stu-id="f22f8-207">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="f22f8-208">**Serwer docelowy**: Podaj nową nazwę serwera mają zostać przywrócone</span><span class="sxs-lookup"><span data-stu-id="f22f8-208">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="f22f8-209">**Lokalizacja**: nie można wybrać region, domyślnie jest taki sam jak serwer źródłowy</span><span class="sxs-lookup"><span data-stu-id="f22f8-209">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="f22f8-210">**Warstwa cenowa**: nie można zmienić tę wartość podczas przywracania serwera.</span><span class="sxs-lookup"><span data-stu-id="f22f8-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="f22f8-211">Jest taki sam jak serwer źródłowy.</span><span class="sxs-lookup"><span data-stu-id="f22f8-211">It is same as the source server.</span></span> 
3.  <span data-ttu-id="f22f8-212">Kliknij przycisk **OK** Aby przywrócić serwer do [Przywracanie do punktu w czasie](./howto-restore-server-portal.md) przed tabele został usunięty.</span><span class="sxs-lookup"><span data-stu-id="f22f8-212">Click **OK** to restore the server to [restore to a point-in-time](./howto-restore-server-portal.md) before the tables was deleted.</span></span> <span data-ttu-id="f22f8-213">Przywracanie serwera do innego punktu w czasie tworzy zduplikowane nowy serwer jako oryginalnego serwera, począwszy od punktu w czasie, możesz określić, pod warunkiem, że w okresie przechowywania dla Twojego [warstwy usług](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-213">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f22f8-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f22f8-214">Next Steps</span></span>
<span data-ttu-id="f22f8-215">W tym samouczku przedstawiono sposób użycia portalu Azure i inne narzędzia do:</span><span class="sxs-lookup"><span data-stu-id="f22f8-215">In this tutorial, you learned how to use the Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f22f8-216">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f22f8-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="f22f8-217">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="f22f8-217">Configure the server firewall</span></span>
> * <span data-ttu-id="f22f8-218">Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie do tworzenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="f22f8-219">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="f22f8-219">Load sample data</span></span>
> * <span data-ttu-id="f22f8-220">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="f22f8-220">Query data</span></span>
> * <span data-ttu-id="f22f8-221">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-221">Update data</span></span>
> * <span data-ttu-id="f22f8-222">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="f22f8-222">Restore data</span></span>

<span data-ttu-id="f22f8-223">Następnie Dowiedz się, jak użyć wiersza polecenia platformy Azure do wykonywania zadań podobne, przejrzyj tego samouczka: [projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f22f8-223">Next, learn how to use Azure CLI to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
