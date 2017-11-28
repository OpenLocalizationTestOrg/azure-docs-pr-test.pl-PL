---
title: "tooAzure aaaConnect bazy danych PostgreSQL używany język PHP | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera przykładowy kod PHP można użyć tooconnect i wyszukiwać dane z bazy danych Azure PostgreSQL."
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
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="02865-103">Bazy danych platformy Azure dla PostgreSQL: Użyj PHP danych tooconnect i zapytań</span><span class="sxs-lookup"><span data-stu-id="02865-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="02865-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych przy użyciu PostgreSQL [PHP](http://php.net/manual/intro-whatis.php) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02865-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="02865-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="02865-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="02865-106">W tym artykule przyjęto założenie, że znasz programowanie za pomocą PHP, ale, czy są nowe tooworking z bazą danych Azure dla PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="02865-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02865-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="02865-107">Prerequisites</span></span>
<span data-ttu-id="02865-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="02865-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="02865-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="02865-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="02865-110">Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="02865-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="02865-111">Instalowanie języka PHP</span><span class="sxs-lookup"><span data-stu-id="02865-111">Install PHP</span></span>
<span data-ttu-id="02865-112">Zainstaluj język PHP na własnym serwerze lub utwórz [aplikację internetową](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview), która zawiera język PHP.</span><span class="sxs-lookup"><span data-stu-id="02865-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="02865-113">Windows</span><span class="sxs-lookup"><span data-stu-id="02865-113">Windows</span></span>
- <span data-ttu-id="02865-114">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="02865-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="02865-115">Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.windows.php) dla dalszego konfiguracji</span><span class="sxs-lookup"><span data-stu-id="02865-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="02865-116">Kod Hello używa hello **pgsql** klasy (ext/php_pgsql.dll), który znajduje się w hello instalacji PHP.</span><span class="sxs-lookup"><span data-stu-id="02865-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="02865-117">Włączone hello **pgsql** rozszerzenia poprzez edycję pliku konfiguracji php.ini hello zazwyczaj znajduje się w `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="02865-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="02865-118">plik konfiguracji Hello powinien zawierać wiersz z tekstem hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="02865-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="02865-119">Jeśli nie jest wyświetlany, Dodaj tekst hello i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="02865-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="02865-120">Jeśli tekst hello jest obecny, ale oznaczone jako z prefiksem średnika, usuń znaczniki komentarza tekst hello przez usunięcie hello średnika.</span><span class="sxs-lookup"><span data-stu-id="02865-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="02865-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="02865-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="02865-122">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="02865-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="02865-123">Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.unix.php) dla dalszego konfiguracji</span><span class="sxs-lookup"><span data-stu-id="02865-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="02865-124">Kod Hello używa hello **pgsql** klasy (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="02865-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="02865-125">Zainstaluj ją, uruchamiając element `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="02865-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="02865-126">Włączone hello **pgsql** rozszerzenia, edytując hello `/etc/php/7.0/mods-available/pgsql.ini` pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="02865-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="02865-127">plik konfiguracji Hello powinien zawierać wiersz z tekstem hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="02865-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="02865-128">Jeśli nie jest wyświetlany, Dodaj tekst hello i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="02865-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="02865-129">Jeśli tekst hello jest obecny, ale oznaczone jako z prefiksem średnika, usuń znaczniki komentarza tekst hello przez usunięcie hello średnika.</span><span class="sxs-lookup"><span data-stu-id="02865-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="02865-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="02865-130">MacOS</span></span>
- <span data-ttu-id="02865-131">Pobierz [język PHP w wersji 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="02865-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="02865-132">Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.macosx.php) dla dalszego konfiguracji</span><span class="sxs-lookup"><span data-stu-id="02865-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="02865-133">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="02865-133">Get connection information</span></span>
<span data-ttu-id="02865-134">Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="02865-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="02865-135">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="02865-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="02865-136">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02865-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="02865-137">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="02865-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="02865-138">Kliknij nazwę serwera hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="02865-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="02865-139">Wybierz powitania serwera **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="02865-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="02865-140">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="02865-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="02865-141">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="02865-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="02865-142">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="02865-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="02865-143">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="02865-143">Connect and create a table</span></span>
<span data-ttu-id="02865-144">Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="02865-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="02865-145">Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="02865-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="02865-146">A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun kilka razy kilku poleceń i [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpi błąd zawsze.</span><span class="sxs-lookup"><span data-stu-id="02865-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="02865-147">A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="02865-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="02865-148">Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="02865-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

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

## <a name="read-data"></a><span data-ttu-id="02865-149">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="02865-149">Read data</span></span>
<span data-ttu-id="02865-150">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="02865-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="02865-151">Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="02865-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="02865-152">A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello wybierz polecenie utrzymywanie hello wyniki w zestawie wyników i [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="02865-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="02865-153">zestaw wyników hello tooread, Metoda [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) jest wywoływana w pętlę, gdy na wiersz i wiersz hello dane są pobierane w tablicy `$row`, z jednego danych wartości w kolumnie w każdej pozycji tablicy.</span><span class="sxs-lookup"><span data-stu-id="02865-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="02865-154">zestaw wyników hello toofree, Metoda [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="02865-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="02865-155">A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="02865-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="02865-156">Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="02865-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
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

## <a name="update-data"></a><span data-ttu-id="02865-157">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="02865-157">Update data</span></span>
<span data-ttu-id="02865-158">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="02865-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="02865-159">Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="02865-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="02865-160">A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun polecenia, a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="02865-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="02865-161">A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="02865-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="02865-162">Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="02865-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

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


## <a name="delete-data"></a><span data-ttu-id="02865-163">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="02865-163">Delete data</span></span>
<span data-ttu-id="02865-164">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="02865-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="02865-165">Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect zbyt Azure bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="02865-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="02865-166">A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun polecenia, a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="02865-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="02865-167">A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="02865-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="02865-168">Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="02865-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

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

## <a name="next-steps"></a><span data-ttu-id="02865-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02865-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="02865-170">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="02865-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
