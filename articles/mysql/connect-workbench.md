---
title: "Łączenia z bazą danych Azure dla programu MySQL z MySQL Workbench | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera czynności w celu MySQL Workbench do nawiązywania połączeń i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="7b441-103">Bazy danych platformy Azure dla programu MySQL: MySQL Workbench używany do nawiązywania połączeń i zapytania na danych</span><span class="sxs-lookup"><span data-stu-id="7b441-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="7b441-104">Ta opcja szybkiego startu pokazuje, jak nawiązać połączenia z bazą danych Azure dla programu MySQL przy użyciu aplikacji MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="7b441-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7b441-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7b441-105">Prerequisites</span></span>
<span data-ttu-id="7b441-106">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="7b441-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="7b441-107">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b441-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="7b441-108">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7b441-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="7b441-109">Zainstaluj narzędzia Workbench MySQL</span><span class="sxs-lookup"><span data-stu-id="7b441-109">Install MySQL Workbench</span></span>
<span data-ttu-id="7b441-110">Pobierz i zainstaluj MySQL Workbench na komputerze z [MySQL witryny sieci Web](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="7b441-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="7b441-111">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="7b441-111">Get connection information</span></span>
<span data-ttu-id="7b441-112">Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="7b441-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="7b441-113">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="7b441-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="7b441-114">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b441-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="7b441-115">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="7b441-115">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="7b441-116">Kliknij nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="7b441-116">Click the server name.</span></span>

4. <span data-ttu-id="7b441-117">Wybierz stronę **Właściwości** serwera.</span><span class="sxs-lookup"><span data-stu-id="7b441-117">Select the server's **Properties** page.</span></span> <span data-ttu-id="7b441-118">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="7b441-118">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Bazy danych platformy Azure dla nazwy serwera MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="7b441-120">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="7b441-120">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-to-the-server-using-mysql-workbench"></a><span data-ttu-id="7b441-121">Połącz z serwerem przy użyciu narzędzia MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="7b441-121">Connect to the server using MySQL Workbench</span></span> 
<span data-ttu-id="7b441-122">Aby nawiązać połączenie z serwerem usługi Azure MySQL za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="7b441-122">To connect to Azure MySQL server using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="7b441-123">Uruchamianie aplikacji MySQL Workbench na komputerze.</span><span class="sxs-lookup"><span data-stu-id="7b441-123">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="7b441-124">W **instalacji nowego połączenia** okna dialogowego wprowadź następujące informacje **parametry** karty:</span><span class="sxs-lookup"><span data-stu-id="7b441-124">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![konfigurowanie nowego połączenia](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="7b441-126">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="7b441-126">**Setting**</span></span> | <span data-ttu-id="7b441-127">**Sugerowana wartość**</span><span class="sxs-lookup"><span data-stu-id="7b441-127">**Suggested value**</span></span> | <span data-ttu-id="7b441-128">**Opis pola**</span><span class="sxs-lookup"><span data-stu-id="7b441-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="7b441-129">Nazwa połączenia</span><span class="sxs-lookup"><span data-stu-id="7b441-129">Connection Name</span></span> | <span data-ttu-id="7b441-130">Połączenie demonstracyjne</span><span class="sxs-lookup"><span data-stu-id="7b441-130">Demo Connection</span></span> | <span data-ttu-id="7b441-131">Podaj etykietę dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="7b441-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="7b441-132">Metoda połączenia</span><span class="sxs-lookup"><span data-stu-id="7b441-132">Connection Method</span></span> | <span data-ttu-id="7b441-133">Standardowa (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="7b441-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="7b441-134">Metoda Standardowa (TCP/IP) jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="7b441-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="7b441-135">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="7b441-135">Hostname</span></span> | <span data-ttu-id="7b441-136">*nazwa serwera*</span><span class="sxs-lookup"><span data-stu-id="7b441-136">*server name*</span></span> | <span data-ttu-id="7b441-137">Określ wartość nazwy serwera, która została użyta wcześniej podczas tworzenia usługi Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="7b441-137">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="7b441-138">Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj w pełni kwalifikowanej nazwy domeny (\*.mysql.database.azure.com) tak jak pokazano w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7b441-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="7b441-139">Postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia, jeśli nie pamiętasz nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="7b441-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="7b441-140">Port</span><span class="sxs-lookup"><span data-stu-id="7b441-140">Port</span></span> | <span data-ttu-id="7b441-141">3306</span><span class="sxs-lookup"><span data-stu-id="7b441-141">3306</span></span> | <span data-ttu-id="7b441-142">Zawsze używaj portu 3306 podczas łączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="7b441-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="7b441-143">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="7b441-143">Username</span></span> |  <span data-ttu-id="7b441-144">*nazwa logowania administratora serwera*</span><span class="sxs-lookup"><span data-stu-id="7b441-144">*server admin login name*</span></span> | <span data-ttu-id="7b441-145">Wpisz nazwę logowania administratora serwera, którą podano wcześniej podczas tworzenia usługi Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="7b441-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="7b441-146">Przykładowa nazwa użytkownika to myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="7b441-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="7b441-147">Postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia, jeśli nie pamiętasz nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b441-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="7b441-148">Format to *username@servername*.</span><span class="sxs-lookup"><span data-stu-id="7b441-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="7b441-149">Hasło</span><span class="sxs-lookup"><span data-stu-id="7b441-149">Password</span></span> | <span data-ttu-id="7b441-150">Twoje hasło</span><span class="sxs-lookup"><span data-stu-id="7b441-150">your password</span></span> | <span data-ttu-id="7b441-151">Kliknij przycisk **magazynu w magazynie...**  przycisk, aby zapisać hasło.</span><span class="sxs-lookup"><span data-stu-id="7b441-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="7b441-152">Kliknij przycisk **Testuj połączenie**, aby sprawdzić, czy wszystkie parametry zostały prawidłowo skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="7b441-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="7b441-153">Kliknij przycisk **OK** można zapisać połączenia.</span><span class="sxs-lookup"><span data-stu-id="7b441-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="7b441-154">Na liście z **połączeń MySQL**, kliknij odpowiadający serwera i poczekaj, aby ustanowić połączenie.</span><span class="sxs-lookup"><span data-stu-id="7b441-154">In the listing of **MySQL Connections**, click the tile corresponding to your server and wait for the connection to be established.</span></span>

6.   <span data-ttu-id="7b441-155">Otwiera nową kartę SQL za pomocą edytora puste można wpisać zapytań.</span><span class="sxs-lookup"><span data-stu-id="7b441-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7b441-156">Domyślnie zabezpieczeń połączenia SSL jest wymagany i wymuszane MySQL serwera bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="7b441-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="7b441-157">Zwykle dodatkowa konfiguracja, z certyfikatów SSL nie jest wymagane dla środowiska roboczego MySQL, aby połączyć się z serwerem.</span><span class="sxs-lookup"><span data-stu-id="7b441-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server.</span></span> <span data-ttu-id="7b441-158">Aby uzyskać więcej informacji dotyczących protokołu SSL, zobacz [łączności Konfigurowanie protokołu SSL w celu bezpiecznego łączenia z bazą danych Azure dla programu MySQL aplikacji](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="7b441-158">For more information on SSL, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="7b441-159">Jeśli potrzebujesz wyłączyć protokół SSL, można znaleźć w portalu Azure, a następnie kliknij przycisk Strona zabezpieczeń połączeń wyłączenie przycisku przełącznika połączenia SSL wymuszania.</span><span class="sxs-lookup"><span data-stu-id="7b441-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="7b441-160">Utwórz tabelę, wstawiania danych, odczytywanie danych, aktualizowanie danych i usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="7b441-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="7b441-161">Skopiuj i wklej przykładowy kod SQL w puste karcie SQL w celu zilustrowania przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="7b441-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="7b441-162">Ten kod tworzy pustą bazę danych o nazwie quickstartdb, a następnie tworzy Przykładowa tabela o nazwie spisu.</span><span class="sxs-lookup"><span data-stu-id="7b441-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="7b441-163">Następnie niektóre wiersze do wstawienia odczytuje wiersze.</span><span class="sxs-lookup"><span data-stu-id="7b441-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="7b441-164">Zmiany danych za pomocą instrukcji update i odczytuje wiersze ponownie.</span><span class="sxs-lookup"><span data-stu-id="7b441-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="7b441-165">Na koniec go usuwa wiersz i odczytuje wiersze ponownie.</span><span class="sxs-lookup"><span data-stu-id="7b441-165">Finally it deletes a row, and reads the rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="7b441-166">Zrzut ekranu przedstawia przykładowy kod SQL w SQL Workbench i dane wyjściowe po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="7b441-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![MySQL Workbench SQL kartę, aby uruchomić przykładowy kod SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="7b441-168">Aby uruchomić przykładowy kod SQL, kliknij przycisk rozjaśnianego ikonę na pasku narzędzi **pliku SQL** kartę.</span><span class="sxs-lookup"><span data-stu-id="7b441-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="7b441-169">Zwróć uwagę, trzy karty wyników w **Siatka wyników** sekcji środku strony.</span><span class="sxs-lookup"><span data-stu-id="7b441-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="7b441-170">Powiadomienie **dane wyjściowe** listy w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="7b441-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="7b441-171">Zostanie wyświetlony stan każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7b441-171">The status of each command is shown.</span></span> 

<span data-ttu-id="7b441-172">Teraz ma połączonej z bazą danych Azure dla programu MySQL przy użyciu narzędzia MySQL Workbench i wykonano zapytanie danych przy użyciu języka SQL.</span><span class="sxs-lookup"><span data-stu-id="7b441-172">Now, you have connected to Azure Database for MySQL using MySQL Workbench, and have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b441-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b441-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7b441-174">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="7b441-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
