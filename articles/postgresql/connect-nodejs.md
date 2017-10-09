---
title: "Połącz tooAzure bazy danych dla PostgreSQL w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera przykładowy kod Node.js można użyć tooconnect i wyszukiwać dane z bazy danych Azure PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla PostgreSQL: Node.js Użyj tooconnect i zapytań danych.
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych przy użyciu PostgreSQL [Node.js](https://nodejs.org/). Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu środowiska Node.js i czy są nowe tooworking z bazą danych Azure dla PostgreSQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie bazy danych — portal](quickstart-create-server-database-portal.md)
- [Tworzenie bazy danych — interfejs wiersza polecenia](quickstart-create-server-database-azure-cli.md)

Należy również:
- Zainstalować środowisko [Node.js](https://nodejs.org).

## <a name="install-pg-client"></a>Instalowanie klienta pg
Zainstaluj [pg](https://www.npmjs.com/package/pg), który jest klientem PostgreSQL dla środowiska Node.js.

toodo tak, uruchom Menedżera pakietów hello węzła (npm) dla języka JavaScript z wiersza polecenia tooinstall hello pg klienta.
```bash
npm install pg
```

Sprawdź listę zainstalowanych pakietów hello hello instalacji.
```bash
npm list
```

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera został utworzony.
3. Kliknij nazwę serwera hello.
4. Wybierz powitania serwera **omówienie** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-nodejs/1-connection-string.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>Wykonywanie kodu JavaScript hello w środowisku Node.js
Może uruchomić Node.js z hello bash powłoki windows wiersza polecenia lub wpisując `node`, interaktywne uruchamianie hello przykładowy kod JavaScript przez kopiowanie i wklejanie w wierszu hello. Alternatywnie możesz zapisać do pliku tekstowego, a następnie uruchom kod JavaScript hello `node filename.js` z nazwą pliku hello jako toorun parametru go.

## <a name="connect-create-table-and-insert-data"></a>Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych
Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL.
Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt. Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera. Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL. 

Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt. Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera. Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL. 

Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL. Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt. Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera. Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL. 

Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt. Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera. Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL. 

Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./howto-migrate-using-export-and-import.md)
