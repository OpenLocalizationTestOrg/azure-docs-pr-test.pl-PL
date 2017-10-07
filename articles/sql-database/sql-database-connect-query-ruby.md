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
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Użyj dopisków fonetycznych tooquery bazy danych Azure SQL

Tego samouczka szybkiego startu przedstawia sposób toouse [Ruby](https://www.ruby-lang.org) toocreate tooan tooconnect programu Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tym szybki start samouczka, upewnij się, że masz hello następujące wymagania wstępne:

- Baza danych Azure SQL. To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start: 

   - [Tworzenie bazy danych — portal](sql-database-get-started-portal.md)
   - [Tworzenie bazy danych — interfejs wiersza polecenia](sql-database-get-started-cli.md)
   - [Tworzenie bazy danych — PowerShell](sql-database-get-started-powershell.md)

- A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.
- W systemie operacyjnym zainstalowano język Ruby i związane z nim oprogramowanie.
    - **System MacOS**: zainstaluj pakiet Homebrew, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS. Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **System Ubuntu**: zainstaluj oprogramowanie wymagane przez język Ruby, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS. Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Informacje o połączeniu z serwerem SQL

Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database. Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 
3. Na powitania **omówienie** stron dla bazy danych, przejrzyj hello pełni kwalifikowaną nazwę serwera. Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji, jak pokazano w powitania po obrazu:

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Jeśli pamiętasz hello informacje logowania dla serwera bazy danych SQL Azure, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera i, w razie potrzeby zresetowania hasła hello.

> [!IMPORTANT]
> W przypadku hello publiczny adres IP komputera hello, na którym jest wykonywana w tym samouczku, musi mieć reguły zapory. Jeśli na innym komputerze lub inny publiczny adres IP, należy utworzyć [reguły zapory poziomu serwera przy użyciu hello portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Wstaw baza danych SQL tooquery kodu

1. W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.rb**

2. Zamień zawartość hello hello następujący kod i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.

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

## <a name="run-hello-code"></a>Uruchamianie hello kodu

1. W wierszu polecenia hello uruchom następujące polecenia hello:

   ```bash
   ruby sqltest.rb
   ```

2. Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.


## <a name="next-steps"></a>Następne kroki
- [Projektowanie pierwszej bazy danych SQL na platformie Azure](sql-database-design-first-database.md)
- [Repozytorium GitHub dla rozwiązania TinyTDS](https://github.com/rails-sqlserver/tiny_tds)
- [Zgłoś problemy lub zadaj pytania dotyczące rozwiązania TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Sterowniki języka Ruby dla platformy SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
