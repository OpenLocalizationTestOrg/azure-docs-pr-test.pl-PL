---
title: "Połącz tooAzure bazy danych dla programu MySQL w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera kilka przykładów kodu Node.js, można użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
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
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="49fd3-103">Bazy danych platformy Azure dla programu MySQL: Node.js Użyj tooconnect i zapytań danych.</span><span class="sxs-lookup"><span data-stu-id="49fd3-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="49fd3-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu [Node.js](https://nodejs.org/) z systemu Windows, Ubuntu Linux i komputerów Mac platform.</span><span class="sxs-lookup"><span data-stu-id="49fd3-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="49fd3-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="49fd3-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="49fd3-106">Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu środowiska Node.js i czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49fd3-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="49fd3-107">Prerequisites</span></span>
<span data-ttu-id="49fd3-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="49fd3-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="49fd3-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="49fd3-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="49fd3-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="49fd3-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="49fd3-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="49fd3-111">You also need to:</span></span>
- <span data-ttu-id="49fd3-112">Zainstaluj hello [Node.js](https://nodejs.org) środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="49fd3-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="49fd3-113">Zainstaluj [mysql2](https://www.npmjs.com/package/mysql2) pakietu tooMySQL tooconnect z hello aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="49fd3-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="49fd3-114">Zainstaluj środowisko Node.js i hello MySQL łącznika</span><span class="sxs-lookup"><span data-stu-id="49fd3-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="49fd3-115">W zależności od platformy należy wykonać tooinstall odpowiednie instrukcje hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="49fd3-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="49fd3-116">Za pomocą programu npm tooinstall hello mysql2 pakiet i jego zależności do folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="49fd3-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="49fd3-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="49fd3-117">**Windows**</span></span>
1. <span data-ttu-id="49fd3-118">Odwiedź hello [Node.js pobiera strony](https://nodejs.org/en/download/) i wybierz z odpowiednią opcję Instalatora systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="49fd3-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="49fd3-119">Utwórz lokalny folder projektu, taki jak `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="49fd3-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="49fd3-120">Uruchom wiersz polecenia hello, dysku cd w folderze projektu hello, takich jak`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="49fd3-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="49fd3-121">Uruchom hello NPM narzędzie tooinstall hello mysql2 biblioteki w folderze projektu hello.</span><span class="sxs-lookup"><span data-stu-id="49fd3-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="49fd3-122">Sprawdź instalacji hello hello `npm list` output tekst `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="49fd3-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="49fd3-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="49fd3-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="49fd3-124">Witaj uruchom następujące polecenia tooinstall **Node.js** i **npm** hello Menedżer pakietów dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="49fd3-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="49fd3-125">Uruchom następujące polecenia toomake hello folderu projektu `mysqlnodejs` i zainstaluj pakiet mysql2 hello do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="49fd3-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="49fd3-126">Sprawdź instalacji hello tekstu wyjściowego listy npm dla `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="49fd3-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="49fd3-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="49fd3-127">**Mac OS**</span></span>
1. <span data-ttu-id="49fd3-128">Wprowadź następujące polecenia tooinstall hello **brew**, Menedżer pakietów łatwy w użyciu dla systemu Mac OS X i **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="49fd3-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="49fd3-129">Uruchom następujące polecenia toomake hello folderu projektu `mysqlnodejs` i zainstaluj pakiet mysql2 hello do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="49fd3-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="49fd3-130">Sprawdź instalacji hello hello `npm list` output tekst `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="49fd3-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="49fd3-131">Witaj numer wersji może się różnić nowe poprawki zostaną zwolnione.</span><span class="sxs-lookup"><span data-stu-id="49fd3-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="49fd3-132">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="49fd3-132">Get connection information</span></span>
<span data-ttu-id="49fd3-133">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="49fd3-134">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="49fd3-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="49fd3-135">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="49fd3-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="49fd3-136">W okienku po lewej stronie powitania kliknij **wszystkie zasoby**, a następnie wyszukaj serwera hello utworzono (na przykład **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="49fd3-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="49fd3-137">Kliknij nazwę serwera hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="49fd3-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="49fd3-138">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="49fd3-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="49fd3-139">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="49fd3-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="49fd3-140">![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="49fd3-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="49fd3-141">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="49fd3-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="49fd3-142">Wykonywanie kodu JavaScript hello w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="49fd3-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="49fd3-143">Wklej kod JavaScript hello do plików tekstowych i zapisać w folderze projektu z js rozszerzenia plików, takich jak C:\nodejsmysql\createtable.js lub /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="49fd3-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="49fd3-144">Uruchom wiersz polecenia hello lub powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="49fd3-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="49fd3-145">Zmień katalog na folder projektu `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="49fd3-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="49fd3-146">Aplikacja hello toorun, wpisz polecenie węzła hello następuje nazwa pliku hello, takich jak `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="49fd3-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="49fd3-147">W systemie Windows Jeśli hello węzła aplikacji nie znajduje się w ścieżce zmiennej środowiskowej może być konieczne toouse hello pełną ścieżkę toolaunch hello węzła aplikacji, takich jak`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="49fd3-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="49fd3-148">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="49fd3-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="49fd3-149">Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="49fd3-150">Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda.</span><span class="sxs-lookup"><span data-stu-id="49fd3-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="49fd3-151">Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) funkcja jest używana tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="49fd3-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="49fd3-152">Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) funkcja jest używana tooexecute hello zapytanie SQL bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="49fd3-153">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="49fd3-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="49fd3-154">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="49fd3-154">Read data</span></span>
<span data-ttu-id="49fd3-155">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="49fd3-156">Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda.</span><span class="sxs-lookup"><span data-stu-id="49fd3-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="49fd3-157">Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) metoda jest używane tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="49fd3-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="49fd3-158">Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) metoda to zapytanie SQL hello tooexecute używana baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="49fd3-159">Tablica wyników Hello jest używany toohold hello wyniki zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="49fd3-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="49fd3-160">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="49fd3-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="49fd3-161">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="49fd3-161">Update data</span></span>
<span data-ttu-id="49fd3-162">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="49fd3-163">Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda.</span><span class="sxs-lookup"><span data-stu-id="49fd3-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="49fd3-164">Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) metoda jest używane tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="49fd3-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="49fd3-165">Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) metoda to zapytanie SQL hello tooexecute używana baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="49fd3-166">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="49fd3-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="49fd3-167">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="49fd3-167">Delete data</span></span>
<span data-ttu-id="49fd3-168">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="49fd3-169">Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda.</span><span class="sxs-lookup"><span data-stu-id="49fd3-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="49fd3-170">Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) metoda jest używane tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="49fd3-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="49fd3-171">Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) metoda to zapytanie SQL hello tooexecute używana baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="49fd3-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="49fd3-172">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="49fd3-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49fd3-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49fd3-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="49fd3-174">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="49fd3-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
