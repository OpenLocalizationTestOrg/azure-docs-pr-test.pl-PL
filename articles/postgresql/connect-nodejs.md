---
title: "Nawiązywanie połączeń z usługą Azure Database for PostgreSQL z poziomu środowiska Node.js | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera przykładowy kod Node.js, którego można używać do nawiązywania połączeń z danymi usługi Azure Database for PostgreSQL i wykonywania zapytań względem nich."
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
ms.openlocfilehash: f6c98833c73b70bcf1f8ca53596a34f09807b276
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="a6dcf-103">Usługa Azure Database for PostgreSQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="a6dcf-103">Azure Database for PostgreSQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="a6dcf-104">Ta opcja szybkiego startu pokazano, jak nawiązać połączenia z bazą danych Azure dla przy użyciu PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="a6dcf-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="a6dcf-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="a6dcf-106">W krokach w tym artykule założono, że wiesz już, jak programować za pomocą języka Node.js, i dopiero zaczynasz pracę z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6dcf-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a6dcf-107">Prerequisites</span></span>
<span data-ttu-id="a6dcf-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="a6dcf-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="a6dcf-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="a6dcf-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="a6dcf-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a6dcf-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="a6dcf-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="a6dcf-111">You also need to:</span></span>
- <span data-ttu-id="a6dcf-112">Zainstalować środowisko [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a6dcf-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="a6dcf-113">Instalowanie klienta pg</span><span class="sxs-lookup"><span data-stu-id="a6dcf-113">Install pg client</span></span>
<span data-ttu-id="a6dcf-114">Zainstaluj [pg](https://www.npmjs.com/package/pg), który jest klientem PostgreSQL dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="a6dcf-115">W tym celu uruchom narzędzie Node Package Manager (npm) dla języka JavaScript z poziomu wiersza polecenia, aby zainstalować klienta pg.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-115">To do so, run the node package manager (npm) for JavaScript from your command line to install the pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="a6dcf-116">Zweryfikuj instalację, wyświetlając listę zainstalowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-116">Verify the installation by listing the packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="a6dcf-117">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="a6dcf-117">Get connection information</span></span>
<span data-ttu-id="a6dcf-118">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-118">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a6dcf-119">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a6dcf-120">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6dcf-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a6dcf-121">Z menu po lewej stronie w portalu Azure kliknij **wszystkie zasoby** i wyszukiwania na serwerze, który został właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-121">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created.</span></span>
3. <span data-ttu-id="a6dcf-122">Kliknij nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-122">Click the server name.</span></span>
4. <span data-ttu-id="a6dcf-123">Wybierz stronę serwera **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-123">Select the server's **Overview** page.</span></span> <span data-ttu-id="a6dcf-124">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-124">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a6dcf-125">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="a6dcf-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="a6dcf-126">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-126">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="a6dcf-127">Uruchamianie kodu JavaScript w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="a6dcf-127">Running the JavaScript code in Node.js</span></span>
<span data-ttu-id="a6dcf-128">Środowisko Node.js można uruchomić w wierszu polecenia powłoki bash lub systemu Windows, wpisując polecenie `node`, a następnie uruchomić przykładowy kod JavaScript przez skopiowanie i wklejenie go w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-128">You may launch Node.js from the bash shell or windows command prompt by typing `node`, then run the example JavaScript code interactively by copy and pasting it onto the prompt.</span></span> <span data-ttu-id="a6dcf-129">Alternatywnie można zapisać kod JavaScript w pliku tekstowym, a następnie uruchomić polecenie `node filename.js` z nazwą pliku jako parametrem uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-129">Alternatively, you may save the JavaScript code into a text file and launch `node filename.js` with the file name as a parameter to run it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="a6dcf-130">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="a6dcf-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="a6dcf-131">Użyj poniższego kodu, aby nawiązać połączenie i załadować dane przy użyciu instrukcji **CREATE TABLE** i **INSERT INTO** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-131">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="a6dcf-132">Obiekt [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) służy do połączenia interfejsem z serwerem programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-132">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="a6dcf-133">Funkcja [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-133">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="a6dcf-134">Funkcja [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) służy do wykonywania zapytania SQL względem bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-134">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="a6dcf-135">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-135">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="a6dcf-136">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="a6dcf-136">Read data</span></span>
<span data-ttu-id="a6dcf-137">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-137">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="a6dcf-138">Obiekt [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) służy do połączenia interfejsem z serwerem programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-138">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="a6dcf-139">Funkcja [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-139">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="a6dcf-140">Funkcja [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) służy do wykonywania zapytania SQL względem bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-140">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="a6dcf-141">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-141">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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
  
    console.log(`Running query to PostgreSQL server: ${config.host}`);

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

## <a name="update-data"></a><span data-ttu-id="a6dcf-142">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="a6dcf-142">Update data</span></span>
<span data-ttu-id="a6dcf-143">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-143">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="a6dcf-144">Obiekt [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) służy do połączenia interfejsem z serwerem programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-144">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="a6dcf-145">Funkcja [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-145">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="a6dcf-146">Funkcja [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) służy do wykonywania zapytania SQL względem bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-146">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="a6dcf-147">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-147">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="a6dcf-148">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="a6dcf-148">Delete data</span></span>
<span data-ttu-id="a6dcf-149">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-149">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="a6dcf-150">Obiekt [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) służy do połączenia interfejsem z serwerem programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-150">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="a6dcf-151">Funkcja [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) służy do nawiązywania połączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-151">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="a6dcf-152">Funkcja [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) służy do wykonywania zapytania SQL względem bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-152">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="a6dcf-153">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a6dcf-153">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="a6dcf-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6dcf-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a6dcf-155">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="a6dcf-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
