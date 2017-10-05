---
title: "Korzystanie z języka PHP do wykonywania zapytań w bazie danych Azure SQL | Microsoft Docs"
description: "W tym temacie przedstawiono sposób użycia języka PHP do utworzenia programu, który nawiązuje połączenie z bazą danych SQL Azure i wykonuje zapytania za pomocą instrukcji języka Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a43472ad2be4a0fd6f7126f72433acd8b5f25fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-php-to-query-an-azure-sql-database"></a><span data-ttu-id="55bc9-103">Korzystanie z języka PHP do wykonywania zapytań w bazie danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="55bc9-103">Use PHP to query an Azure SQL database</span></span>

<span data-ttu-id="55bc9-104">W tym przewodniku Szybki start pokazano, jak używać języka [PHP](http://php.net/manual/en/intro-whatis.php) w celu utworzenia programu służącego do nawiązywania połączenia z bazą danych Azure SQL, a następnie, korzystając z instrukcji Transact-SQL, wysyłać zapytania o dane.</span><span class="sxs-lookup"><span data-stu-id="55bc9-104">This quick start tutorial demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55bc9-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55bc9-105">Prerequisites</span></span>

<span data-ttu-id="55bc9-106">Aby ukończyć ten samouczek Szybki start, upewnij się, że dysponujesz następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="55bc9-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="55bc9-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55bc9-107">An Azure SQL database.</span></span> <span data-ttu-id="55bc9-108">Ten przewodnik Szybki start używa zasobów utworzonych w jednym z poniższych przewodników Szybki start:</span><span class="sxs-lookup"><span data-stu-id="55bc9-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="55bc9-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="55bc9-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="55bc9-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="55bc9-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="55bc9-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="55bc9-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="55bc9-112">[Reguła zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla publicznego adresu IP komputera, który będzie używany w tym samouczku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="55bc9-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="55bc9-113">W systemie operacyjnym zainstalowano język PHP i związane z nim oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="55bc9-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="55bc9-114">**System MacOS**: zainstaluj oprogramowania Homebrew i PHP, zainstaluj sterownik ODBC i pakiet SQLCMD, a następnie zainstaluj sterownik języka PHP dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="55bc9-114">**MacOS**: Install Homebrew and PHP, install the ODBC driver and SQLCMD, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="55bc9-115">Zobacz [kroki 1.2, 1.3 i 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="55bc9-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="55bc9-116">**System Ubuntu**: zainstaluj język PHP i inne wymagane pakiety, a następnie zainstaluj sterownik języka PHP dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="55bc9-116">**Ubuntu**:  Install PHP and other required packages, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="55bc9-117">Zobacz [kroki 1.2 i 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="55bc9-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="55bc9-118">**System Windows**: zainstaluj najnowszą wersję programu PHP dla usług IIS Express, najnowszą wersja sterowników firmy Microsoft dla programu SQL Server w usługach IIS Express, Chocolatey, sterownik ODBC i pakiet SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="55bc9-118">**Windows**: Install the newest version of PHP for IIS Express, the newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, the ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="55bc9-119">Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="55bc9-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="55bc9-120">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="55bc9-120">SQL server connection information</span></span>

<span data-ttu-id="55bc9-121">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z bazą danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55bc9-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="55bc9-122">W następnych procedurach będą potrzebne w pełni kwalifikowana nazwa serwera, nazwa bazy danych i informacje logowania.</span><span class="sxs-lookup"><span data-stu-id="55bc9-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="55bc9-123">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="55bc9-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="55bc9-124">Wybierz opcję **Bazy danych SQL** z menu po lewej stronie, a następnie kliknij bazę danych na stronie **Bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="55bc9-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="55bc9-125">Na stronie **Przegląd** bazy danych zweryfikuj w pełni kwalifikowaną nazwę serwera, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="55bc9-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="55bc9-126">Możesz umieścić kursor na nazwie serwera w celu wywołania opcji **Kliknij, aby skopiować**.</span><span class="sxs-lookup"><span data-stu-id="55bc9-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="55bc9-128">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony serwera usługi SQL Database, aby wyświetlić nazwę administratora serwera oraz, w razie konieczności, zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="55bc9-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="55bc9-129">Wstawianie kodu zapytania bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="55bc9-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="55bc9-130">W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="55bc9-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="55bc9-131">Zastąp jego zawartość następującym kodem i dodaj odpowiednie wartości dla serwera, bazy danych, użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="55bc9-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes the connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-the-code"></a><span data-ttu-id="55bc9-132">Uruchamianie kodu</span><span class="sxs-lookup"><span data-stu-id="55bc9-132">Run the code</span></span>

1. <span data-ttu-id="55bc9-133">W wierszu polecenia uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="55bc9-133">At the command prompt, run the following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="55bc9-134">Sprawdź, czy zostało zwróconych 20 pierwszych wierszy, a następnie zamknij okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55bc9-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55bc9-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55bc9-135">Next steps</span></span>
- [<span data-ttu-id="55bc9-136">Projektowanie pierwszej bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="55bc9-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="55bc9-137">Sterowniki [PHP firmy Microsoft dla programu SQL Server](https://github.com/Microsoft/msphpsql/)</span><span class="sxs-lookup"><span data-stu-id="55bc9-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/)</span></span>
- [<span data-ttu-id="55bc9-138">Zgłaszanie problemów/zadawanie pytań</span><span class="sxs-lookup"><span data-stu-id="55bc9-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
