---
title: aaaUse Node.js tooquery bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "W tym temacie opisano sposób toouse Node.js toocreate program, który łączy tooan bazy danych SQL Azure i zapytania za pomocą instrukcji języka Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="af000-103">Użyj tooquery Node.js bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="af000-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="af000-104">Tego samouczka szybkiego startu przedstawia sposób toouse [Node.js](https://nodejs.org/en/) toocreate tooan tooconnect programu Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="af000-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af000-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af000-105">Prerequisites</span></span>

<span data-ttu-id="af000-106">toocomplete tym szybki start samouczka, upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="af000-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="af000-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="af000-107">An Azure SQL database.</span></span> <span data-ttu-id="af000-108">To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="af000-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="af000-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="af000-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="af000-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="af000-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="af000-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="af000-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="af000-112">A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.</span><span class="sxs-lookup"><span data-stu-id="af000-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="af000-113">W systemie operacyjnym zainstalowano narzędzie Node.js i związane z nim oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="af000-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="af000-114">**System MacOS**: Instalowanie oprogramowania Homebrew i Node.js, a następnie zainstalować sterownik ODBC hello i użycia programu SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="af000-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="af000-115">Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="af000-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="af000-116">**Ubuntu**: zainstaluj środowisko Node.js, a następnie zainstalować sterownik ODBC hello i użycia programu SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="af000-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="af000-117">Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="af000-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="af000-118">**Windows**: Zainstaluj Chocolatey i Node.js, a następnie zainstaluj hello sterownika ODBC i SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="af000-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="af000-119">Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="af000-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="af000-120">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="af000-120">SQL server connection information</span></span>

<span data-ttu-id="af000-121">Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="af000-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="af000-122">Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.</span><span class="sxs-lookup"><span data-stu-id="af000-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="af000-123">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="af000-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="af000-124">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="af000-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="af000-125">Na powitania **omówienie** stron dla bazy danych, przejrzyj hello w pełni kwalifikowana nazwa serwera, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="af000-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="af000-126">Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.</span><span class="sxs-lookup"><span data-stu-id="af000-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="af000-128">Jeśli pamiętasz hello informacje logowania dla serwera bazy danych SQL Azure, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera i, w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="af000-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af000-129">W przypadku hello publiczny adres IP komputera hello, na którym jest wykonywana w tym samouczku, musi mieć reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="af000-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="af000-130">Jeśli na innym komputerze lub inny publiczny adres IP, należy utworzyć [reguły zapory poziomu serwera przy użyciu hello portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="af000-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="af000-131">Tworzenie projektu z użyciem narzędzia Node.js</span><span class="sxs-lookup"><span data-stu-id="af000-131">Create a Node.js project</span></span>

<span data-ttu-id="af000-132">Otwórz wiersz polecenia i utwórz folder o nazwie *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="af000-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="af000-133">Przejdź toohello folder utworzony i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="af000-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="af000-134">Wstaw baza danych SQL tooquery kodu</span><span class="sxs-lookup"><span data-stu-id="af000-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="af000-135">W środowisku projektowym lub ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="af000-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="af000-136">Zamień zawartość hello hello następujący kod i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="af000-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a><span data-ttu-id="af000-137">Uruchamianie hello kodu</span><span class="sxs-lookup"><span data-stu-id="af000-137">Run hello code</span></span>

1. <span data-ttu-id="af000-138">W wierszu polecenia hello uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="af000-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="af000-139">Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="af000-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af000-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af000-140">Next steps</span></span>

- <span data-ttu-id="af000-141">Dowiedz się więcej o hello [Microsoft Driver Node.js dla programu SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="af000-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="af000-142">Dowiedz się, jak za[połączenia i wykonywać zapytania bazy danych Azure SQL przy użyciu platformy .NET core](sql-database-connect-query-dotnet-core.md) na Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="af000-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="af000-143">Dowiedz się więcej o [Rozpoczynanie pracy z platformą .NET Core na Windows/Linux/macOS przy użyciu wiersza polecenia hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="af000-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="af000-144">Dowiedz się, jak za[projektowania pierwszą bazę danych Azure SQL przy użyciu narzędzia SSMS](sql-database-design-first-database.md) lub [projektowania pierwszą bazę danych Azure SQL przy użyciu platformy .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="af000-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="af000-145">Dowiedz się, jak za[Connect i zapytanie z SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="af000-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="af000-146">Dowiedz się, jak za[Connect i zapytanie z kodem Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="af000-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


