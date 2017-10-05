---
title: "Nawiązywanie połączeń z usługą Azure Database for PostgreSQL za pomocą języka PHP | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera przykładowy kod PHP, którego można używać do nawiązywania połączeń z danymi usługi Azure Database for PostgreSQL i wykonywania zapytań względem nich."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="07af8-103">Usługa Azure Database for PostgreSQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="07af8-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="07af8-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for PostgreSQL przy użyciu aplikacji języka [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="07af8-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="07af8-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="07af8-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="07af8-106">W tym artykule założono, że wiesz już, jak programować za pomocą języka PHP, i dopiero zaczynasz pracę z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07af8-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07af8-107">Prerequisites</span></span>
<span data-ttu-id="07af8-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="07af8-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="07af8-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="07af8-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="07af8-110">Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="07af8-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="07af8-111">Instalowanie języka PHP</span><span class="sxs-lookup"><span data-stu-id="07af8-111">Install PHP</span></span>
<span data-ttu-id="07af8-112">Zainstaluj język PHP na własnym serwerze lub utwórz [aplikację internetową](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview), która zawiera język PHP.</span><span class="sxs-lookup"><span data-stu-id="07af8-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="07af8-113">Windows</span><span class="sxs-lookup"><span data-stu-id="07af8-113">Windows</span></span>
- <span data-ttu-id="07af8-114">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="07af8-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="07af8-115">Zainstaluj język PHP i zapoznaj się z [podręcznikiem języka PHP](http://php.net/manual/install.windows.php) w celu przeprowadzenia dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="07af8-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="07af8-116">Kod używa klasy **pgsql** (ext/php_pgsql.dll) uwzględnionej w instalacji języka PHP.</span><span class="sxs-lookup"><span data-stu-id="07af8-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="07af8-117">Włącz rozszerzenie **pgsql**, edytując plik konfiguracji php.ini, który zazwyczaj znajduje się w folderze `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="07af8-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="07af8-118">Plik konfiguracji powinien zawierać wiersz z tekstem `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="07af8-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="07af8-119">Jeśli nie jest wyświetlany, dodaj tekst i zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="07af8-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="07af8-120">Jeśli tekst jest wyświetlany, ale zawiera komentarz z prefiksem ze średnikiem, usuń komentarz z tekstu, usuwając średnik.</span><span class="sxs-lookup"><span data-stu-id="07af8-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="07af8-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="07af8-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="07af8-122">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="07af8-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="07af8-123">Zainstaluj język PHP i zapoznaj się z [podręcznikiem języka PHP](http://php.net/manual/install.unix.php) w celu przeprowadzenia dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="07af8-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="07af8-124">Kod używa klasy **pgsql** (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="07af8-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="07af8-125">Zainstaluj ją, uruchamiając element `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="07af8-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="07af8-126">Włącz rozszerzenie **pgsql**, edytując plik konfiguracji `/etc/php/7.0/mods-available/pgsql.ini`.</span><span class="sxs-lookup"><span data-stu-id="07af8-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="07af8-127">Plik konfiguracji powinien zawierać wiersz z tekstem `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="07af8-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="07af8-128">Jeśli nie jest wyświetlany, dodaj tekst i zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="07af8-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="07af8-129">Jeśli tekst jest wyświetlany, ale zawiera komentarz z prefiksem ze średnikiem, usuń komentarz z tekstu, usuwając średnik.</span><span class="sxs-lookup"><span data-stu-id="07af8-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="07af8-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="07af8-130">MacOS</span></span>
- <span data-ttu-id="07af8-131">Pobierz [język PHP w wersji 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="07af8-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="07af8-132">Zainstaluj język PHP i zapoznaj się z [podręcznikiem języka PHP](http://php.net/manual/install.macosx.php) w celu przeprowadzenia dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="07af8-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="07af8-133">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="07af8-133">Get connection information</span></span>
<span data-ttu-id="07af8-134">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="07af8-135">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="07af8-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="07af8-136">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="07af8-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="07af8-137">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="07af8-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="07af8-138">Kliknij nazwę serwera **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="07af8-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="07af8-139">Wybierz stronę serwera **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="07af8-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="07af8-140">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="07af8-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="07af8-141">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="07af8-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="07af8-142">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="07af8-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="07af8-143">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="07af8-143">Connect and create a table</span></span>
<span data-ttu-id="07af8-144">Użyj poniższego kodu w celu nawiązania połączenia i utworzenia tabeli za pomocą instrukcji **CREATE TABLE** języka SQL, a następnie instrukcji **INSERT INTO** języka SQL, aby dodać wiersze do tabeli.</span><span class="sxs-lookup"><span data-stu-id="07af8-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="07af8-145">Kod wywołuje metodę [pg_connect()](http://php.net/manual/en/function.pg-connect.php), aby nawiązać połączenie z usługą Azure for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="07af8-146">Następnie kod wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) kilka razy w celu uruchomienia wielu poleceń i metodę [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) w celu sprawdzenia szczegółów, jeśli za każdym razem występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="07af8-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="07af8-147">W kolejnym kroku kod wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) w celu zamknięcia połączenia.</span><span class="sxs-lookup"><span data-stu-id="07af8-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="07af8-148">Zastąp parametry `$host`, `$database`, `$user` i `$password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="07af8-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="07af8-149">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="07af8-149">Read data</span></span>
<span data-ttu-id="07af8-150">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="07af8-151">Kod wywołuje metodę [pg_connect()](http://php.net/manual/en/function.pg-connect.php), aby nawiązać połączenie z usługą Azure for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="07af8-152">Następnie kod wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) w celu uruchomienia polecenia SELECT, zachowując wyniki w zestawie wyników, i metodę [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) w celu sprawdzenia błędów, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="07af8-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="07af8-153">Aby odczytać zestaw wyników, metoda [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) jest wywoływana w postaci pętli, jeden raz dla każdego wiersza, a dane są pobierane w tablicy `$row`, z jedną wartością danych na kolumnę w każdej pozycji tablicy.</span><span class="sxs-lookup"><span data-stu-id="07af8-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="07af8-154">Aby zwolnić zestaw wyników, należy wywołać metodę [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php).</span><span class="sxs-lookup"><span data-stu-id="07af8-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="07af8-155">W kolejnym kroku kod wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) w celu zamknięcia połączenia.</span><span class="sxs-lookup"><span data-stu-id="07af8-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="07af8-156">Zastąp parametry `$host`, `$database`, `$user` i `$password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="07af8-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="07af8-157">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="07af8-157">Update data</span></span>
<span data-ttu-id="07af8-158">Użyj poniższego kodu, aby nawiązać połączenie i zaktualizować dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="07af8-159">Kod wywołuje metodę [pg_connect()](http://php.net/manual/en/function.pg-connect.php), aby nawiązać połączenie z usługą Azure for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="07af8-160">Następnie kod wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) w celu uruchomienia polecenia i metodę [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) w celu sprawdzenia szczegółów, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="07af8-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="07af8-161">W kolejnym kroku kod wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) w celu zamknięcia połączenia.</span><span class="sxs-lookup"><span data-stu-id="07af8-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="07af8-162">Zastąp parametry `$host`, `$database`, `$user` i `$password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="07af8-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="07af8-163">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="07af8-163">Delete data</span></span>
<span data-ttu-id="07af8-164">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="07af8-165">Kod wywołuje metodę [pg_connect()](http://php.net/manual/en/function.pg-connect.php), aby nawiązać połączenie z usługą Azure for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07af8-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="07af8-166">Następnie kod wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) w celu uruchomienia polecenia i metodę [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) w celu sprawdzenia szczegółów, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="07af8-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="07af8-167">W kolejnym kroku kod wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) w celu zamknięcia połączenia.</span><span class="sxs-lookup"><span data-stu-id="07af8-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="07af8-168">Zastąp parametry `$host`, `$database`, `$user` i `$password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="07af8-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="07af8-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07af8-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="07af8-170">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="07af8-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
