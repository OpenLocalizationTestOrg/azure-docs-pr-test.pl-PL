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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="068d4-103">Bazy danych platformy Azure dla programu MySQL: Użyj PHP danych tooconnect i zapytań</span><span class="sxs-lookup"><span data-stu-id="068d4-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="068d4-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu [PHP](http://php.net/manual/intro-whatis.php) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="068d4-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="068d4-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="068d4-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="068d4-106">W tym artykule przyjęto założenie, że znasz programowanie za pomocą PHP, ale, czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="068d4-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="068d4-107">Prerequisites</span></span>
<span data-ttu-id="068d4-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="068d4-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="068d4-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="068d4-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="068d4-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="068d4-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="068d4-111">Instalowanie języka PHP</span><span class="sxs-lookup"><span data-stu-id="068d4-111">Install PHP</span></span>
<span data-ttu-id="068d4-112">Zainstaluj język PHP na własnym serwerze lub utwórz [aplikację internetową](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview), która zawiera język PHP.</span><span class="sxs-lookup"><span data-stu-id="068d4-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="068d4-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="068d4-113">MacOS</span></span>
- <span data-ttu-id="068d4-114">Pobierz [język PHP w wersji 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="068d4-115">Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.macosx.php) dla dalszego konfiguracji</span><span class="sxs-lookup"><span data-stu-id="068d4-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="068d4-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="068d4-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="068d4-117">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="068d4-118">Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.unix.php) dla dalszego konfiguracji</span><span class="sxs-lookup"><span data-stu-id="068d4-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="068d4-119">Windows</span><span class="sxs-lookup"><span data-stu-id="068d4-119">Windows</span></span>
- <span data-ttu-id="068d4-120">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="068d4-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="068d4-121">Instalowanie języka PHP i odwoływać się toohello [ręcznego PHP](http://php.net/manual/install.windows.php) dla dalszego konfiguracji</span><span class="sxs-lookup"><span data-stu-id="068d4-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="068d4-122">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="068d4-122">Get connection information</span></span>
<span data-ttu-id="068d4-123">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="068d4-124">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="068d4-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="068d4-125">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="068d4-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="068d4-126">W okienku po lewej stronie powitania kliknij **wszystkie zasoby**, a następnie wyszukaj serwera hello utworzono (na przykład **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="068d4-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="068d4-127">Kliknij nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="068d4-127">Click hello server name.</span></span>
4. <span data-ttu-id="068d4-128">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="068d4-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="068d4-129">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="068d4-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="068d4-130">![Nazwa serwera usługi Azure Database for MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="068d4-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="068d4-131">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="068d4-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="068d4-132">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="068d4-132">Connect and create a table</span></span>
<span data-ttu-id="068d4-133">Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="068d4-134">Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="068d4-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="068d4-135">Witaj kodu wywołania metody [mysqli_init](http://php.net/manual/mysqli.init.php) i [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="068d4-136">A następnie wywołuje metodę [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="068d4-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="068d4-137">A następnie wywołuje metodę [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="068d4-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="068d4-138">Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="068d4-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="068d4-139">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="068d4-139">Insert data</span></span>
<span data-ttu-id="068d4-140">Użyj hello następujący kod tooconnect i wstawianie danych przy użyciu **Wstaw** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="068d4-141">Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="068d4-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="068d4-142">Witaj kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate przygotowane instrukcja insert, a następnie wiązania hello parametry dla każdej wartości wstawionych kolumny za pomocą metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="068d4-143">Kod Hello jest uruchamiany przy użyciu metody instrukcji hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) , a następnie zamyka hello instrukcję, używając metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="068d4-144">Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="068d4-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="068d4-145">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="068d4-145">Read data</span></span>
<span data-ttu-id="068d4-146">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="068d4-147">Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="068d4-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="068d4-148">Witaj kod używa metody [mysqli_query](http://php.net/manual/mysqli.query.php) wykonać zapytania sql hello i używa [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch metody hello zwrócone wiersze.</span><span class="sxs-lookup"><span data-stu-id="068d4-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="068d4-149">Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="068d4-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="068d4-150">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="068d4-150">Update data</span></span>
<span data-ttu-id="068d4-151">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="068d4-152">Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="068d4-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="068d4-153">Witaj kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate instrukcji update przygotowane, czym wiąże hello parametry dla każdej wartości w kolumnie zaktualizowane przy użyciu metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="068d4-154">Kod Hello jest uruchamiany przy użyciu metody instrukcji hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) , a następnie zamyka hello instrukcję, używając metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="068d4-155">Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="068d4-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="068d4-156">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="068d4-156">Delete data</span></span>
<span data-ttu-id="068d4-157">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="068d4-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="068d4-158">Kod Hello używa hello **MySQL ulepszone rozszerzenie** klasy (mysqli) zawarte w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="068d4-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="068d4-159">Witaj kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate przygotowane instrukcja delete, a następnie wiązania hello parametrów hello gdzie klauzula w instrukcji hello przy użyciu metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="068d4-160">Kod Hello jest uruchamiany przy użyciu metody instrukcji hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) , a następnie zamyka hello instrukcję, używając metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="068d4-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="068d4-161">Zastąp parametry hosta, nazwę użytkownika, hasło i db_name hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="068d4-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="068d4-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="068d4-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="068d4-163">Kompilowanie aplikacji internetowej języka PHP i MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="068d4-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
