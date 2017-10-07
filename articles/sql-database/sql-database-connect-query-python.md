---
title: aaaUse Python tooquery bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "W tym temacie opisano sposób toouse Python toocreate program, który łączy tooan bazy danych SQL Azure i zapytania za pomocą instrukcji języka Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="a6a0b-103">Użyj tooquery Python bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="a6a0b-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="a6a0b-104">To szybki start pokazano, jak toouse [Python](https://python.org) tooan tooconnect Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6a0b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a6a0b-105">Prerequisites</span></span>

<span data-ttu-id="a6a0b-106">toocomplete tym szybki start samouczka, upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a6a0b-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="a6a0b-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-107">An Azure SQL database.</span></span> <span data-ttu-id="a6a0b-108">To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="a6a0b-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="a6a0b-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="a6a0b-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="a6a0b-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a6a0b-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="a6a0b-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6a0b-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="a6a0b-112">A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="a6a0b-113">W systemie operacyjnym zainstalowano język Python i związane z nim oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="a6a0b-114">**System MacOS**: zainstalowania oprogramowania Homebrew i Python, instalowania sterownika ODBC: hello i SQLCMD, a następnie zainstaluj hello sterownik języka Python dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="a6a0b-115">Zobacz [kroki 1.2, 1.3 i 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="a6a0b-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="a6a0b-116">**Ubuntu**: Zainstaluj Python i inne wymagane pakiety i hello instalacji sterowników języka Python dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="a6a0b-117">Zobacz [kroki 1.2, 1.3 i 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="a6a0b-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="a6a0b-118">**Windows**: Zainstaluj hello najnowszą wersję języka Python (zmiennej środowiskowej jest teraz skonfigurowane dla Ciebie), instalowania sterownika ODBC: hello i SQLCMD, a następnie zainstaluj hello sterownik języka Python dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="a6a0b-119">Zobacz [kroki 1.2, 1.3 i 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="a6a0b-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="a6a0b-120">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="a6a0b-120">SQL server connection information</span></span>

<span data-ttu-id="a6a0b-121">Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="a6a0b-122">Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="a6a0b-123">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6a0b-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a6a0b-124">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="a6a0b-125">Na powitania **omówienie** stron dla bazy danych, przejrzyj hello w pełni kwalifikowana nazwa serwera, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="a6a0b-126">Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="a6a0b-128">Jeśli zapomnisz informacje logowania serwera, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera i, w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="a6a0b-129">Wstaw baza danych SQL tooquery kodu</span><span class="sxs-lookup"><span data-stu-id="a6a0b-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="a6a0b-130">W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.rb**.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="a6a0b-131">Zamień zawartość hello hello następujący kod i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="a6a0b-132">Uruchamianie hello kodu</span><span class="sxs-lookup"><span data-stu-id="a6a0b-132">Run hello code</span></span>

1. <span data-ttu-id="a6a0b-133">W wierszu polecenia hello uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a6a0b-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="a6a0b-134">Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a6a0b-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6a0b-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6a0b-135">Next steps</span></span>

- [<span data-ttu-id="a6a0b-136">Projektowanie pierwszej bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a6a0b-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="a6a0b-137">Sterowniki Microsoft Python dla platformy SQL Server</span><span class="sxs-lookup"><span data-stu-id="a6a0b-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="a6a0b-138">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="a6a0b-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

