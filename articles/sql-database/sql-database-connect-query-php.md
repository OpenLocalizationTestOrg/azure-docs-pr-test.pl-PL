---
title: aaaUse PHP tooquery bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "W tym temacie opisano sposób toouse PHP toocreate program, który łączy tooan bazy danych SQL Azure i zapytania za pomocą instrukcji języka Transact-SQL."
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
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a>Użyj tooquery PHP bazy danych Azure SQL

Tego samouczka szybkiego startu przedstawia sposób toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan tooconnect programu Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tym szybki start samouczka, upewnij się, że masz następujące hello:

- Baza danych Azure SQL. To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start: 

   - [Tworzenie bazy danych — portal](sql-database-get-started-portal.md)
   - [Tworzenie bazy danych — interfejs wiersza polecenia](sql-database-get-started-cli.md)
   - [Tworzenie bazy danych — PowerShell](sql-database-get-started-powershell.md)

- A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.

- W systemie operacyjnym zainstalowano język PHP i związane z nim oprogramowanie.

    - **System MacOS**: zainstalowania oprogramowania Homebrew i PHP, instalowania sterownika ODBC: hello i SQLCMD, a następnie zainstaluj hello sterowników PHP dla programu SQL Server. Zobacz [kroki 1.2, 1.3 i 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: zainstalować PHP i inne wymagane pakiety i hello instalacji sterowników PHP dla programu SQL Server. Zobacz [kroki 1.2 i 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: Zainstaluj hello najnowszą wersję PHP dla usług IIS Express, najnowsza wersja hello Drivers firmy Microsoft dla programu SQL Server w usługi IIS Express, Chocolatey hello sterownika ODBC i SQLCMD. Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>Informacje o połączeniu z serwerem SQL

Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database. Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 
3. Na powitania **omówienie** stron dla bazy danych, przejrzyj hello w pełni kwalifikowana nazwa serwera, pokazane na powitania po obrazu. Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.  

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Jeśli zapomnisz informacje logowania serwera, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera i, w razie potrzeby zresetowania hasła hello.     
    
## <a name="insert-code-tooquery-sql-database"></a>Wstaw baza danych SQL tooquery kodu

1. W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.php**.  

2. Zamień zawartość hello hello następujący kod i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
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

## <a name="run-hello-code"></a>Uruchamianie hello kodu

1. W wierszu polecenia hello uruchom następujące polecenia hello:

   ```php
   php sqltest.php
   ```

2. Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.

## <a name="next-steps"></a>Następne kroki
- [Projektowanie pierwszej bazy danych SQL na platformie Azure](sql-database-design-first-database.md)
- Sterowniki [PHP firmy Microsoft dla programu SQL Server](https://github.com/Microsoft/msphpsql/)
- [Zgłaszanie problemów/zadawanie pytań](https://github.com/Microsoft/msphpsql/issues)
