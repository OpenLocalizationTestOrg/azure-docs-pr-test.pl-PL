---
title: "Połącz tooAzure bazy danych dla programu MySQL za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera kilka przykładów kodu PHP, możesz użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: Użyj PHP danych tooconnect i zapytań
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu [PHP](http://php.net/manual/intro-whatis.php) aplikacji. Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. W tym artykule przyjęto założenie, że znasz programowanie za pomocą PHP, ale, czy są nowe tooworking z bazą danych Azure dla programu MySQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>Instalowanie języka PHP
Zainstaluj język PHP na własnym serwerze lub utwórz [aplikację internetową](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview), która zawiera język PHP.

### <a name="macos"></a>MacOS
- Pobierz [język PHP w wersji 7.1.4](http://php.net/downloads.php).
- Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.macosx.php) dla dalszego konfiguracji

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://php.net/downloads.php).
- Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.unix.php) dla dalszego konfiguracji

### <a name="windows"></a>Windows
- Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://windows.php.net/download#php-7.1).
- Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.windows.php) dla dalszego konfiguracji

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. W okienku po lewej stronie powitania kliknij **wszystkie zasoby**, a następnie wyszukaj serwera hello utworzono (na przykład **myserver4demo**).
3. Kliknij nazwę serwera hello.
4. Wybierz powitania serwera **właściwości** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Nazwa serwera usługi Azure Database for MySQL](./media/connect-php/1_server-properties-name-login.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="connect-and-create-a-table"></a>Łączenie i tworzenie tabeli
Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL. 

Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP. Witaj kodu wywołania metody [mysqli_init](http://php.net/manual/mysqli.init.php) i [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. A następnie wywołuje metodę [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello zapytania. A następnie wywołuje metodę [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello połączenia.

Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Wstawianie danych
Użyj hello następujący kod tooconnect i wstawianie danych przy użyciu **Wstaw** instrukcji SQL.

Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP. Witaj kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate przygotowane instrukcja insert, a następnie wiązania hello parametry dla każdej wartości wstawionych kolumny za pomocą metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Kod Hello jest uruchamiany przy użyciu metody instrukcji hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) , a następnie zamyka hello instrukcję, używając metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.  Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP. Witaj kod używa metody [mysqli_query](http://php.net/manual/mysqli.query.php) wykonać zapytania sql hello i używa [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch metody hello zwrócone wiersze.

Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.

Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP. Witaj kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate instrukcji update przygotowane, czym wiąże hello parametry dla każdej wartości w kolumnie zaktualizowane przy użyciu metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Kod Hello jest uruchamiany przy użyciu metody instrukcji hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) , a następnie zamyka hello instrukcję, używając metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. 

Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP. Witaj kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate przygotowane instrukcja delete, a następnie wiązania hello parametrów hello gdzie klauzula w instrukcji hello przy użyciu metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Kod Hello jest uruchamiany przy użyciu metody instrukcji hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) , a następnie zamyka hello instrukcję, używając metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Kompilowanie aplikacji internetowej języka PHP i MySQL na platformie Azure](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
