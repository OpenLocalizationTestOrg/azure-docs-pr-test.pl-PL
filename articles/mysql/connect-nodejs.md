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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: Node.js Użyj tooconnect i zapytań danych.
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu [Node.js](https://nodejs.org/) z systemu Windows, Ubuntu Linux i komputerów Mac platform. Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu środowiska Node.js i czy są nowe tooworking z bazą danych Azure dla programu MySQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

Należy również:
- Zainstaluj hello [Node.js](https://nodejs.org) środowiska wykonawczego.
- Zainstaluj [mysql2](https://www.npmjs.com/package/mysql2) pakietu tooMySQL tooconnect z hello aplikacji Node.js. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Zainstaluj środowisko Node.js i hello MySQL łącznika
W zależności od platformy należy wykonać tooinstall odpowiednie instrukcje hello Node.js. Za pomocą programu npm tooinstall hello mysql2 pakiet i jego zależności do folderu projektu.

### <a name="windows"></a>**Windows**
1. Odwiedź hello [Node.js pobiera strony](https://nodejs.org/en/download/) i wybierz z odpowiednią opcję Instalatora systemu Windows.
2. Utwórz lokalny folder projektu, taki jak `nodejsmysql`. 
3. Uruchom wiersz polecenia hello, dysku cd w folderze projektu hello, takich jak`cd c:\nodejsmysql\`
4. Uruchom hello NPM narzędzie tooinstall hello mysql2 biblioteki w folderze projektu hello.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Sprawdź instalacji hello hello `npm list` output tekst `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Witaj uruchom następujące polecenia tooinstall **Node.js** i **npm** hello Menedżer pakietów dla środowiska Node.js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Uruchom następujące polecenia toomake hello folderu projektu `mysqlnodejs` i zainstaluj pakiet mysql2 hello do tego folderu.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Sprawdź instalacji hello tekstu wyjściowego listy npm dla `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Wprowadź następujące polecenia tooinstall hello **brew**, Menedżer pakietów łatwy w użyciu dla systemu Mac OS X i **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Uruchom następujące polecenia toomake hello folderu projektu `mysqlnodejs` i zainstaluj pakiet mysql2 hello do tego folderu.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Sprawdź instalacji hello hello `npm list` output tekst `mysql2@1.3.6`. Witaj numer wersji może się różnić nowe poprawki zostaną zwolnione.

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. W okienku po lewej stronie powitania kliknij **wszystkie zasoby**, a następnie wyszukaj serwera hello utworzono (na przykład **myserver4demo**).
3. Kliknij nazwę serwera hello **myserver4demo**.
4. Wybierz powitania serwera **właściwości** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-nodejs/1_server-properties-name-login.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>Wykonywanie kodu JavaScript hello w środowisku Node.js
1. Wklej kod JavaScript hello do plików tekstowych i zapisać w folderze projektu z js rozszerzenia plików, takich jak C:\nodejsmysql\createtable.js lub /home/username/nodejsmysql/createtable.js
2. Uruchom wiersz polecenia hello lub powłoki bash. Zmień katalog na folder projektu `cd nodejsmysql`.
3. Aplikacja hello toorun, wpisz polecenie węzła hello następuje nazwa pliku hello, takich jak `node createtable.js`.
4. W systemie Windows Jeśli hello węzła aplikacji nie znajduje się w ścieżce zmiennej środowiskowej może być konieczne toouse hello pełną ścieżkę toolaunch hello węzła aplikacji, takich jak`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych
Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL.

Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda. Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) funkcja jest używana tooestablish hello połączenia toohello serwera. Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) funkcja jest używana tooexecute hello zapytanie SQL bazy danych MySQL. 

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. 

Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda. Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) metoda jest używane tooestablish hello połączenia toohello serwera. Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) metoda to zapytanie SQL hello tooexecute używana baza danych MySQL. Tablica wyników Hello jest używany toohold hello wyniki zapytania hello.

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL. 

Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda. Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) metoda jest używane tooestablish hello połączenia toohello serwera. Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) metoda to zapytanie SQL hello tooexecute używana baza danych MySQL. 

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. 

Witaj [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) toointerface używane z serwerem MySQL hello jest metoda. Witaj [connect()](https://github.com/mysqljs/mysql#establishing-connections) metoda jest używane tooestablish hello połączenia toohello serwera. Witaj [query()](https://github.com/mysqljs/mysql#performing-queries) metoda to zapytanie SQL hello tooexecute używana baza danych MySQL. 

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./concepts-migrate-import-export.md)
