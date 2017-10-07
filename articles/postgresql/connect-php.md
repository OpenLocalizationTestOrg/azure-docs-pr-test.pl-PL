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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla PostgreSQL: Użyj PHP danych tooconnect i zapytań
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych przy użyciu PostgreSQL [PHP](http://php.net/manual/intro-whatis.php) aplikacji. Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. W tym artykule przyjęto założenie, że znasz programowanie za pomocą PHP, ale, czy są nowe tooworking z bazą danych Azure dla PostgreSQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie bazy danych — portal](quickstart-create-server-database-portal.md)
- [Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Instalowanie języka PHP
Zainstaluj język PHP na własnym serwerze lub utwórz [aplikację internetową](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview), która zawiera język PHP.

### <a name="windows"></a>Windows
- Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://windows.php.net/download#php-7.1).
- Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.windows.php) dla dalszego konfiguracji
- Kod Hello używa hello **pgsql** klasy (ext/php_pgsql.dll), który znajduje się w hello instalacji PHP. 
- Włączone hello **pgsql** rozszerzenia poprzez edycję pliku konfiguracji php.ini hello zazwyczaj znajduje się w `C:\Program Files\PHP\v7.1\php.ini`. plik konfiguracji Hello powinien zawierać wiersz z tekstem hello `extension=php_pgsql.so`. Jeśli nie jest wyświetlany, Dodaj tekst hello i Zapisz plik hello. Jeśli tekst hello jest obecny, ale oznaczone jako z prefiksem średnika, usuń znaczniki komentarza tekst hello przez usunięcie hello średnika.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://php.net/downloads.php). 
- Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.unix.php) dla dalszego konfiguracji
- Kod Hello używa hello **pgsql** klasy (php_pgsql.so). Zainstaluj ją, uruchamiając element `sudo apt-get install php-pgsql`.
- Włączone hello **pgsql** rozszerzenia, edytując hello `/etc/php/7.0/mods-available/pgsql.ini` pliku konfiguracji. plik konfiguracji Hello powinien zawierać wiersz z tekstem hello `extension=php_pgsql.so`. Jeśli nie jest wyświetlany, Dodaj tekst hello i Zapisz plik hello. Jeśli tekst hello jest obecny, ale oznaczone jako z prefiksem średnika, usuń znaczniki komentarza tekst hello przez usunięcie hello średnika.

### <a name="macos"></a>MacOS
- Pobierz [język PHP w wersji 7.1.4](http://php.net/downloads.php).
- Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.macosx.php) dla dalszego konfiguracji

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **mypgserver 20170401**.
3. Kliknij nazwę serwera hello **mypgserver 20170401**.
4. Wybierz powitania serwera **omówienie** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-php/1-connection-string.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="connect-and-create-a-table"></a>Łączenie i tworzenie tabeli
Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.

Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun kilka razy kilku poleceń i [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpi błąd zawsze. A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.

Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości. 

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

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. 

 Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello wybierz polecenie utrzymywanie hello wyniki w zestawie wyników i [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpił błąd.  zestaw wyników hello tooread, Metoda [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) jest wywoływana w pętlę, gdy na wiersz i wiersz hello dane są pobierane w tablicy `$row`, z jednego danych wartości w kolumnie w każdej pozycji tablicy.  zestaw wyników hello toofree, Metoda [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) jest wywoływana. A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.

Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości. 

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

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.

Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun polecenia, a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpił błąd. A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.

Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości. 

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


## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. 

 Witaj kodu wywołania metody [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect zbyt Azure bazy danych PostgreSQL. A następnie wywołuje metodę [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun polecenia, a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello szczegółowych informacji, jeśli wystąpił błąd. A następnie wywołuje metodę [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello połączenia.

Zastąp hello `$host`, `$database`, `$user`, i `$password` parametrów z własne wartości. 

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

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./howto-migrate-using-export-and-import.md)
