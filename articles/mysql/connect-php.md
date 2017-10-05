---
title: "Nawiązywanie połączeń z usługą Azure Database for MySQL za pomocą języka PHP | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera kilka przykładów kodu PHP, których można używać do nawiązywania połączeń z danymi usługi Azure Database for MySQL i wykonywania zapytań względem nich."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 59da1ab9e76685d7ed0c4415ef99578c982e956c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="5b817-103">Usługa Azure Database for MySQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="5b817-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="5b817-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for MySQL przy użyciu aplikacji języka [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="5b817-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5b817-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="5b817-106">W tym artykule założono, że wiesz już, jak programować za pomocą języka PHP, i dopiero zaczynasz pracę z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b817-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5b817-107">Prerequisites</span></span>
<span data-ttu-id="5b817-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="5b817-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5b817-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b817-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="5b817-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5b817-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="5b817-111">Instalowanie języka PHP</span><span class="sxs-lookup"><span data-stu-id="5b817-111">Install PHP</span></span>
<span data-ttu-id="5b817-112">Zainstaluj język PHP na własnym serwerze lub utwórz [aplikację internetową](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview), która zawiera język PHP.</span><span class="sxs-lookup"><span data-stu-id="5b817-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="5b817-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="5b817-113">MacOS</span></span>
- <span data-ttu-id="5b817-114">Pobierz [język PHP w wersji 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="5b817-115">Zainstaluj język PHP i zapoznaj się z [podręcznikiem języka PHP](http://php.net/manual/install.macosx.php) w celu przeprowadzenia dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5b817-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5b817-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5b817-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="5b817-117">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="5b817-118">Zainstaluj język PHP i zapoznaj się z [podręcznikiem języka PHP](http://php.net/manual/install.unix.php) w celu przeprowadzenia dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5b817-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="5b817-119">Windows</span><span class="sxs-lookup"><span data-stu-id="5b817-119">Windows</span></span>
- <span data-ttu-id="5b817-120">Pobierz [bezpieczny, niestanowiący zagrożenia język PHP w wersji 7.1.4 (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="5b817-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="5b817-121">Zainstaluj język PHP i zapoznaj się z [podręcznikiem języka PHP](http://php.net/manual/install.windows.php) w celu przeprowadzenia dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5b817-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5b817-122">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="5b817-122">Get connection information</span></span>
<span data-ttu-id="5b817-123">Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="5b817-124">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="5b817-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5b817-125">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b817-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5b817-126">W lewym okienku kliknij pozycję **Wszystkie zasoby**, a następnie wyszukaj utworzony serwer (na przykład **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="5b817-126">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="5b817-127">Kliknij nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="5b817-127">Click the server name.</span></span>
4. <span data-ttu-id="5b817-128">Wybierz stronę **Właściwości** serwera.</span><span class="sxs-lookup"><span data-stu-id="5b817-128">Select the server's **Properties** page.</span></span> <span data-ttu-id="5b817-129">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="5b817-129">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5b817-130">![Nazwa serwera usługi Azure Database for MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5b817-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5b817-131">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="5b817-131">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="5b817-132">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="5b817-132">Connect and create a table</span></span>
<span data-ttu-id="5b817-133">Użyj poniższego kodu w celu nawiązania połączenia i utworzenia tabeli za pomocą instrukcji **CREATE TABLE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-133">Use the following code to connect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="5b817-134">Kod używa klasy **rozszerzenia MySQL Improved** (mysqli) uwzględnionej w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="5b817-134">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5b817-135">Kod wywołuje metody [mysqli_init](http://php.net/manual/mysqli.init.php) i [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) w celu połączenia z systemem MySQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-135">The code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="5b817-136">Następnie wywołuje on metodę [mysqli_query](http://php.net/manual/mysqli.query.php) w celu uruchomienia zapytania.</span><span class="sxs-lookup"><span data-stu-id="5b817-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="5b817-137">W kolejnym kroku kod wywołuje metodę [mysqli_close](http://php.net/manual/mysqli.close.php) w celu zamknięcia połączenia.</span><span class="sxs-lookup"><span data-stu-id="5b817-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="5b817-138">Zastąp parametry hosta, nazwy użytkownika, hasła i nazwy bazy danych własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5b817-138">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
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

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="5b817-139">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="5b817-139">Insert data</span></span>
<span data-ttu-id="5b817-140">Użyj poniższego kodu, aby nawiązać połączenie i wstawić dane za pomocą instrukcji **INSERT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-140">Use the following code to connect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="5b817-141">Kod używa klasy **rozszerzenia MySQL Improved** (mysqli) uwzględnionej w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="5b817-141">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5b817-142">Kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) w celu utworzenia przygotowanej instrukcji insert, a następnie tworzy powiązania parametrów dla każdej wstawionej wartości kolumny za pomocą metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-142">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="5b817-143">Kod uruchamia instrukcję, używając metody [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php), a następnie zamyka instrukcję przy użyciu metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-143">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="5b817-144">Zastąp parametry hosta, nazwy użytkownika, hasła i nazwy bazy danych własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5b817-144">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
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

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="5b817-145">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="5b817-145">Read data</span></span>
<span data-ttu-id="5b817-146">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-146">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="5b817-147">Kod używa klasy **rozszerzenia MySQL Improved** (mysqli) uwzględnionej w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="5b817-147">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5b817-148">Kod używa metody [mysqli_query](http://php.net/manual/mysqli.query.php) w celu wykonania zapytania SQL, a metody [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) — w celu pobrania wynikowych wierszy.</span><span class="sxs-lookup"><span data-stu-id="5b817-148">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method to fetch the resulting rows.</span></span>

<span data-ttu-id="5b817-149">Zastąp parametry hosta, nazwy użytkownika, hasła i nazwy bazy danych własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5b817-149">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="5b817-150">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="5b817-150">Update data</span></span>
<span data-ttu-id="5b817-151">Użyj poniższego kodu, aby nawiązać połączenie i zaktualizować dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-151">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="5b817-152">Kod używa klasy **rozszerzenia MySQL Improved** (mysqli) uwzględnionej w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="5b817-152">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5b817-153">Kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) w celu utworzenia przygotowanej instrukcji update, a następnie tworzy powiązania parametrów dla każdej zaktualizowanej wartości kolumny za pomocą metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-153">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="5b817-154">Kod uruchamia instrukcję, używając metody [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php), a następnie zamyka instrukcję przy użyciu metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-154">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="5b817-155">Zastąp parametry hosta, nazwy użytkownika, hasła i nazwy bazy danych własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5b817-155">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="5b817-156">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="5b817-156">Delete data</span></span>
<span data-ttu-id="5b817-157">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="5b817-157">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="5b817-158">Kod używa klasy **rozszerzenia MySQL Improved** (mysqli) uwzględnionej w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="5b817-158">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5b817-159">Kod używa metody [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) w celu utworzenia przygotowanej instrukcji delete, a następnie tworzy powiązania parametrów dla klauzuli where w instrukcji przy użyciu metody [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-159">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="5b817-160">Kod uruchamia instrukcję, używając metody [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php), a następnie zamyka instrukcję przy użyciu metody [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="5b817-160">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="5b817-161">Zastąp parametry hosta, nazwy użytkownika, hasła i nazwy bazy danych własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5b817-161">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="5b817-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b817-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5b817-163">Kompilowanie aplikacji internetowej języka PHP i MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5b817-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
