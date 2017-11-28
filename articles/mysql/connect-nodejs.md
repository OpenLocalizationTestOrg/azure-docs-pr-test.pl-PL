---
title: "Nawiązywanie połączeń z usługą Azure Database for MySQL z poziomu środowiska Node.js | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera kilka przykładów kodu Node.js, których można używać do nawiązywania połączeń z danymi usługi Azure Database for MySQL i wykonywania zapytań względem nich."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: 0c0bd4b707c114d2991e5f0473a4bfbe9e463e3c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="00a9e-103">Usługa Azure Database for MySQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="00a9e-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="00a9e-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for MySQL przy użyciu języka [Node.js](https://nodejs.org/) na platformach Windows, Ubuntu Linux i Mac.</span><span class="sxs-lookup"><span data-stu-id="00a9e-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="00a9e-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="00a9e-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="00a9e-106">W krokach w tym artykule założono, że wiesz już, jak programować za pomocą języka Node.js, i dopiero zaczynasz pracę z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00a9e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="00a9e-107">Prerequisites</span></span>
<span data-ttu-id="00a9e-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="00a9e-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="00a9e-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00a9e-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="00a9e-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="00a9e-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="00a9e-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="00a9e-111">You also need to:</span></span>
- <span data-ttu-id="00a9e-112">Zainstalować środowisko uruchomieniowe [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="00a9e-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="00a9e-113">Zainstalować pakiet [mysql2](https://www.npmjs.com/package/mysql2) w celu połączenia z programem MySQL z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="00a9e-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="00a9e-114">Instalowanie środowiska Node.js i łącznika programu MySQL</span><span class="sxs-lookup"><span data-stu-id="00a9e-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="00a9e-115">W zależności od platformy wykonaj odpowiednie instrukcje dotyczące instalowania programu Node.js.</span><span class="sxs-lookup"><span data-stu-id="00a9e-115">Depending on your platform, follow the appropriate instructions to install Node.js.</span></span> <span data-ttu-id="00a9e-116">Użyj programu npm, aby zainstalować pakiet mysql2 i jego zależności w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="00a9e-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="00a9e-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="00a9e-117">**Windows**</span></span>
1. <span data-ttu-id="00a9e-118">Odwiedź [stronę pobierania środowiska Node.js](https://nodejs.org/en/download/) i wybierz odpowiednią opcję Instalatora Windows.</span><span class="sxs-lookup"><span data-stu-id="00a9e-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="00a9e-119">Utwórz lokalny folder projektu, taki jak `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="00a9e-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="00a9e-120">Uruchom wiersz polecenia i użyj polecenia cd, aby zmienić katalog na folder projektu, taki jak `cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="00a9e-120">Launch the command prompt and cd into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="00a9e-121">Uruchom narzędzie NPM, aby zainstalować bibliotekę mysql2 w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="00a9e-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="00a9e-122">Sprawdź instalację, sprawdzając tekst danych wyjściowych polecenia `npm list` dla `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="00a9e-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="00a9e-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="00a9e-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="00a9e-124">Uruchom następujące polecenia, aby zainstalować środowisko **Node.js** i program **npm**, czyli menedżera pakietów dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="00a9e-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="00a9e-125">Uruchom następujące polecenia, aby utworzyć folder projektu `mysqlnodejs` i zainstalować pakiet mysql2 w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="00a9e-125">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="00a9e-126">Sprawdź instalację, sprawdzając tekst danych wyjściowych listy npm dla `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="00a9e-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="00a9e-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="00a9e-127">**Mac OS**</span></span>
1. <span data-ttu-id="00a9e-128">Wprowadź następujące polecenia, aby zainstalować rozwiązanie **brew**, czyli łatwy w użyciu menedżer pakietów dla systemu Mac OS X i środowiska **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="00a9e-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="00a9e-129">Uruchom następujące polecenia, aby utworzyć folder projektu `mysqlnodejs` i zainstalować pakiet mysql2 w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="00a9e-129">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="00a9e-130">Sprawdź instalację, sprawdzając tekst danych wyjściowych polecenia `npm list` dla `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="00a9e-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="00a9e-131">Numer wersji może się różnić po wydaniu nowych poprawek.</span><span class="sxs-lookup"><span data-stu-id="00a9e-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="00a9e-132">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="00a9e-132">Get connection information</span></span>
<span data-ttu-id="00a9e-133">Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="00a9e-134">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="00a9e-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="00a9e-135">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="00a9e-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="00a9e-136">W lewym okienku kliknij pozycję **Wszystkie zasoby**, a następnie wyszukaj utworzony serwer (na przykład **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="00a9e-136">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="00a9e-137">Kliknij nazwę serwera **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="00a9e-137">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="00a9e-138">Wybierz stronę **Właściwości** serwera.</span><span class="sxs-lookup"><span data-stu-id="00a9e-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="00a9e-139">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="00a9e-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="00a9e-140">![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="00a9e-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="00a9e-141">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="00a9e-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="00a9e-142">Uruchamianie kodu JavaScript w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="00a9e-142">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="00a9e-143">Wklej kod JavaScript do plików tekstowych i zapisz w folderze projektu z rozszerzeniem js, na przykład C:\nodejsmysql\createtable.js lub /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="00a9e-143">Paste the JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="00a9e-144">Uruchom wiersz polecenia lub powłokę bash.</span><span class="sxs-lookup"><span data-stu-id="00a9e-144">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="00a9e-145">Zmień katalog na folder projektu `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="00a9e-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="00a9e-146">Aby uruchomić aplikację, wpisz polecenie node, a po nim nazwę pliku, taką jak `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="00a9e-146">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="00a9e-147">W systemie Windows, jeśli aplikacja Node nie znajduje się w ścieżce zmiennej środowiskowej, może być konieczne użycie pełnej ścieżki do uruchomienia aplikacji Node, takiej jak `"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="00a9e-147">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="00a9e-148">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="00a9e-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="00a9e-149">Użyj poniższego kodu, aby nawiązać połączenie i załadować dane przy użyciu instrukcji **CREATE TABLE** i **INSERT INTO** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-149">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="00a9e-150">Metoda [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) służy do połączenia interfejsem z serwerem programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-150">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="00a9e-151">Funkcja [connect()](https://github.com/mysqljs/mysql#establishing-connections) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="00a9e-151">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="00a9e-152">Funkcja [query()](https://github.com/mysqljs/mysql#performing-queries) służy do wykonywania zapytania SQL względem bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-152">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="00a9e-153">Zastąp parametry `host`, `user`, `password` i `database` wartościami określonymi podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="00a9e-153">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="00a9e-154">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="00a9e-154">Read data</span></span>
<span data-ttu-id="00a9e-155">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-155">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="00a9e-156">Metoda [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) służy do połączenia interfejsem z serwerem programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-156">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="00a9e-157">Metoda [connect()](https://github.com/mysqljs/mysql#establishing-connections) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="00a9e-157">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="00a9e-158">Metoda [query()](https://github.com/mysqljs/mysql#performing-queries) służy do wykonywania zapytania SQL względem bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-158">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="00a9e-159">Tablica wyników jest używana do przechowywania wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="00a9e-159">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="00a9e-160">Zastąp parametry `host`, `user`, `password` i `database` wartościami określonymi podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="00a9e-160">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="00a9e-161">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="00a9e-161">Update data</span></span>
<span data-ttu-id="00a9e-162">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-162">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="00a9e-163">Metoda [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) służy do połączenia interfejsem z serwerem programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-163">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="00a9e-164">Metoda [connect()](https://github.com/mysqljs/mysql#establishing-connections) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="00a9e-164">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="00a9e-165">Metoda [query()](https://github.com/mysqljs/mysql#performing-queries) służy do wykonywania zapytania SQL względem bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-165">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="00a9e-166">Zastąp parametry `host`, `user`, `password` i `database` wartościami określonymi podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="00a9e-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="00a9e-167">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="00a9e-167">Delete data</span></span>
<span data-ttu-id="00a9e-168">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-168">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="00a9e-169">Metoda [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) służy do połączenia interfejsem z serwerem programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-169">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="00a9e-170">Metoda [connect()](https://github.com/mysqljs/mysql#establishing-connections) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="00a9e-170">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="00a9e-171">Metoda [query()](https://github.com/mysqljs/mysql#performing-queries) służy do wykonywania zapytania SQL względem bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="00a9e-171">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="00a9e-172">Zastąp parametry `host`, `user`, `password` i `database` wartościami określonymi podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="00a9e-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="00a9e-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="00a9e-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="00a9e-174">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="00a9e-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
