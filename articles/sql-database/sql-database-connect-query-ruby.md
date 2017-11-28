---
title: "aaaUse dopisków fonetycznych tooquery bazy danych SQL Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano sposób toouse dopisków fonetycznych toocreate program, który łączy tooan bazy danych SQL Azure i zapytania za pomocą instrukcji języka Transact-SQL."
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
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="4f469-103">Użyj dopisków fonetycznych tooquery bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="4f469-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="4f469-104">Tego samouczka szybkiego startu przedstawia sposób toouse [Ruby](https://www.ruby-lang.org) toocreate tooan tooconnect programu Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4f469-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f469-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f469-105">Prerequisites</span></span>

<span data-ttu-id="4f469-106">toocomplete tym szybki start samouczka, upewnij się, że masz hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="4f469-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="4f469-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4f469-107">An Azure SQL database.</span></span> <span data-ttu-id="4f469-108">To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="4f469-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="4f469-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="4f469-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="4f469-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4f469-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="4f469-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f469-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="4f469-112">A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.</span><span class="sxs-lookup"><span data-stu-id="4f469-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="4f469-113">W systemie operacyjnym zainstalowano język Ruby i związane z nim oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="4f469-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="4f469-114">**System MacOS**: zainstaluj pakiet Homebrew, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="4f469-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="4f469-115">Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="4f469-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="4f469-116">**System Ubuntu**: zainstaluj oprogramowanie wymagane przez język Ruby, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="4f469-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="4f469-117">Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="4f469-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="4f469-118">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="4f469-118">SQL server connection information</span></span>

<span data-ttu-id="4f469-119">Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="4f469-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="4f469-120">Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.</span><span class="sxs-lookup"><span data-stu-id="4f469-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="4f469-121">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f469-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f469-122">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="4f469-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="4f469-123">Na powitania **omówienie** stron dla bazy danych, przejrzyj hello pełni kwalifikowaną nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="4f469-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="4f469-124">Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="4f469-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="4f469-126">Jeśli pamiętasz hello informacje logowania dla serwera bazy danych SQL Azure, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera i, w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="4f469-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f469-127">W przypadku hello publiczny adres IP komputera hello, na którym jest wykonywana w tym samouczku, musi mieć reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="4f469-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="4f469-128">Jeśli na innym komputerze lub inny publiczny adres IP, należy utworzyć [reguły zapory poziomu serwera przy użyciu hello portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="4f469-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="4f469-129">Wstaw baza danych SQL tooquery kodu</span><span class="sxs-lookup"><span data-stu-id="4f469-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="4f469-130">W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="4f469-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="4f469-131">Zamień zawartość hello hello następujący kod i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="4f469-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="4f469-132">Uruchamianie hello kodu</span><span class="sxs-lookup"><span data-stu-id="4f469-132">Run hello code</span></span>

1. <span data-ttu-id="4f469-133">W wierszu polecenia hello uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4f469-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="4f469-134">Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4f469-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f469-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f469-135">Next Steps</span></span>
- [<span data-ttu-id="4f469-136">Projektowanie pierwszej bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4f469-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="4f469-137">Repozytorium GitHub dla rozwiązania TinyTDS</span><span class="sxs-lookup"><span data-stu-id="4f469-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="4f469-138">Zgłoś problemy lub zadaj pytania dotyczące rozwiązania TinyTDS</span><span class="sxs-lookup"><span data-stu-id="4f469-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="4f469-139">Sterowniki języka Ruby dla platformy SQL Server</span><span class="sxs-lookup"><span data-stu-id="4f469-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
