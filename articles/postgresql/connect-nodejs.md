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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="c4d29-103">Bazy danych platformy Azure dla PostgreSQL: Node.js Użyj tooconnect i zapytań danych.</span><span class="sxs-lookup"><span data-stu-id="c4d29-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="c4d29-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych przy użyciu PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="c4d29-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="c4d29-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="c4d29-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="c4d29-106">Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu środowiska Node.js i czy są nowe tooworking z bazą danych Azure dla PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4d29-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c4d29-107">Prerequisites</span></span>
<span data-ttu-id="c4d29-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="c4d29-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c4d29-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="c4d29-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="c4d29-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c4d29-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="c4d29-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="c4d29-111">You also need to:</span></span>
- <span data-ttu-id="c4d29-112">Zainstalować środowisko [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="c4d29-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="c4d29-113">Instalowanie klienta pg</span><span class="sxs-lookup"><span data-stu-id="c4d29-113">Install pg client</span></span>
<span data-ttu-id="c4d29-114">Zainstaluj [pg](https://www.npmjs.com/package/pg), który jest klientem PostgreSQL dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="c4d29-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="c4d29-115">toodo tak, uruchom Menedżera pakietów hello węzła (npm) dla języka JavaScript z wiersza polecenia tooinstall hello pg klienta.</span><span class="sxs-lookup"><span data-stu-id="c4d29-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="c4d29-116">Sprawdź listę zainstalowanych pakietów hello hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="c4d29-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="c4d29-117">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="c4d29-117">Get connection information</span></span>
<span data-ttu-id="c4d29-118">Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d29-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c4d29-119">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="c4d29-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c4d29-120">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4d29-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4d29-121">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c4d29-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="c4d29-122">Kliknij nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="c4d29-122">Click hello server name.</span></span>
4. <span data-ttu-id="c4d29-123">Wybierz powitania serwera **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="c4d29-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="c4d29-124">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="c4d29-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c4d29-125">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="c4d29-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="c4d29-126">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="c4d29-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="c4d29-127">Wykonywanie kodu JavaScript hello w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="c4d29-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="c4d29-128">Może uruchomić Node.js z hello bash powłoki windows wiersza polecenia lub wpisując `node`, interaktywne uruchamianie hello przykładowy kod JavaScript przez kopiowanie i wklejanie w wierszu hello.</span><span class="sxs-lookup"><span data-stu-id="c4d29-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="c4d29-129">Alternatywnie możesz zapisać do pliku tekstowego, a następnie uruchom kod JavaScript hello `node filename.js` z nazwą pliku hello jako toorun parametru go.</span><span class="sxs-lookup"><span data-stu-id="c4d29-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="c4d29-130">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="c4d29-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="c4d29-131">Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="c4d29-132">Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt.</span><span class="sxs-lookup"><span data-stu-id="c4d29-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="c4d29-133">Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c4d29-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="c4d29-134">Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="c4d29-135">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4d29-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="c4d29-136">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="c4d29-136">Read data</span></span>
<span data-ttu-id="c4d29-137">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="c4d29-138">Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt.</span><span class="sxs-lookup"><span data-stu-id="c4d29-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="c4d29-139">Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c4d29-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="c4d29-140">Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="c4d29-141">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4d29-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="c4d29-142">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="c4d29-142">Update data</span></span>
<span data-ttu-id="c4d29-143">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="c4d29-144">Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt.</span><span class="sxs-lookup"><span data-stu-id="c4d29-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="c4d29-145">Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c4d29-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="c4d29-146">Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="c4d29-147">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4d29-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="c4d29-148">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="c4d29-148">Delete data</span></span>
<span data-ttu-id="c4d29-149">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="c4d29-150">Witaj [pg. Klient](https://github.com/brianc/node-postgres/wiki/Client) toointerface używane z serwerem PostgreSQL hello jest obiekt.</span><span class="sxs-lookup"><span data-stu-id="c4d29-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="c4d29-151">Witaj [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funkcja jest używana tooestablish hello połączenia toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c4d29-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="c4d29-152">Witaj [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4d29-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="c4d29-153">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4d29-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="c4d29-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4d29-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c4d29-155">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="c4d29-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
