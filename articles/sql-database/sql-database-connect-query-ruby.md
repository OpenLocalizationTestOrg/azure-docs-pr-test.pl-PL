---
title: "Korzystanie z języka Ruby do wykonywania zapytań w bazie danych Azure SQL | Microsoft Docs"
description: "W tym temacie przedstawiono sposób użycia języka Ruby do utworzenia programu, który nawiązuje połączenie z bazą danych SQL Azure i wykonuje zapytania za pomocą instrukcji języka Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 25ff9a9cfaa5494dbb006c84e235099fe51e6545
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a><span data-ttu-id="61da7-103">Korzystanie z języka Ruby do wykonywania zapytań w bazie danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="61da7-103">Use Ruby to query an Azure SQL database</span></span>

<span data-ttu-id="61da7-104">W tym przewodniku Szybki start pokazano, jak używać języka [Ruby](https://www.ruby-lang.org) w celu utworzenia programu służącego do nawiązywania połączenia z bazą danych Azure SQL, a następnie, korzystając z instrukcji Transact-SQL, wysyłać zapytania o dane.</span><span class="sxs-lookup"><span data-stu-id="61da7-104">This quick start tutorial demonstrates how to use [Ruby](https://www.ruby-lang.org) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61da7-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="61da7-105">Prerequisites</span></span>

<span data-ttu-id="61da7-106">Aby ukończyć ten samouczek Szybki start, upewnij się, że dysponujesz następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="61da7-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="61da7-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="61da7-107">An Azure SQL database.</span></span> <span data-ttu-id="61da7-108">Ten przewodnik Szybki start używa zasobów utworzonych w jednym z poniższych przewodników Szybki start:</span><span class="sxs-lookup"><span data-stu-id="61da7-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="61da7-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="61da7-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="61da7-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="61da7-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="61da7-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="61da7-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="61da7-112">[Reguła zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla publicznego adresu IP komputera, który będzie używany w tym samouczku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="61da7-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="61da7-113">W systemie operacyjnym zainstalowano język Ruby i związane z nim oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="61da7-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="61da7-114">**System MacOS**: zainstaluj pakiet Homebrew, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="61da7-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="61da7-115">Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="61da7-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="61da7-116">**System Ubuntu**: zainstaluj oprogramowanie wymagane przez język Ruby, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="61da7-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="61da7-117">Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="61da7-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="61da7-118">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="61da7-118">SQL server connection information</span></span>

<span data-ttu-id="61da7-119">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z bazą danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="61da7-119">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="61da7-120">W następnych procedurach będą potrzebne w pełni kwalifikowana nazwa serwera, nazwa bazy danych i informacje logowania.</span><span class="sxs-lookup"><span data-stu-id="61da7-120">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="61da7-121">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="61da7-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="61da7-122">Wybierz opcję **Bazy danych SQL** z menu po lewej stronie, a następnie kliknij bazę danych na stronie **Bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="61da7-122">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="61da7-123">Na stronie **Przegląd** bazy danych sprawdź w pełni kwalifikowaną nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="61da7-123">On the **Overview** page for your database, review the fully qualified server name.</span></span> <span data-ttu-id="61da7-124">Możesz umieścić kursor na nazwie serwera w celu wywołania opcji **Kliknij, aby skopiować**, jak pokazano na poniższym rysunku:</span><span class="sxs-lookup"><span data-stu-id="61da7-124">You can hover over the server name to bring up the **Click to copy** option, as shown in the following image:</span></span>

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="61da7-126">Jeśli nie pamiętasz informacji logowania dla serwera Azure SQL Database, przejdź do strony serwera SQL Database, aby wyświetlić nazwę administratora oraz, w razie konieczności, zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="61da7-126">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61da7-127">W przypadku publicznego adresu IP komputera, na którym jest wykonywany ten samouczek, niezbędne jest posiadanie reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="61da7-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="61da7-128">Jeśli pracujesz na innym komputerze lub masz inny publiczny adres IP, utwórz [regułę zapory poziomu serwera przy użyciu portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="61da7-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="61da7-129">Wstawianie kodu zapytania bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="61da7-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="61da7-130">W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="61da7-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="61da7-131">Zastąp jego zawartość następującym kodem i dodaj odpowiednie wartości dla serwera, bazy danych, użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="61da7-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-the-code"></a><span data-ttu-id="61da7-132">Uruchamianie kodu</span><span class="sxs-lookup"><span data-stu-id="61da7-132">Run the code</span></span>

1. <span data-ttu-id="61da7-133">W wierszu polecenia uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="61da7-133">At the command prompt, run the following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="61da7-134">Sprawdź, czy zostało zwróconych 20 pierwszych wierszy, a następnie zamknij okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61da7-134">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="61da7-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61da7-135">Next Steps</span></span>
- [<span data-ttu-id="61da7-136">Projektowanie pierwszej bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="61da7-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="61da7-137">Repozytorium GitHub dla rozwiązania TinyTDS</span><span class="sxs-lookup"><span data-stu-id="61da7-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="61da7-138">Zgłoś problemy lub zadaj pytania dotyczące rozwiązania TinyTDS</span><span class="sxs-lookup"><span data-stu-id="61da7-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="61da7-139">Sterowniki języka Ruby dla platformy SQL Server</span><span class="sxs-lookup"><span data-stu-id="61da7-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
