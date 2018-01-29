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
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: quickstart
ms.date: 07/15/2017
ms.author: carlrab
ms.openlocfilehash: 3427d216540451bc10b968f866d0fce0f6df3c54
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a>Korzystanie z języka Ruby do wykonywania zapytań w bazie danych Azure SQL

W tym przewodniku Szybki start pokazano, jak używać języka [Ruby](https://www.ruby-lang.org) w celu utworzenia programu służącego do nawiązywania połączenia z bazą danych Azure SQL, a następnie, korzystając z instrukcji Transact-SQL, wysyłać zapytania o dane.

## <a name="prerequisites"></a>Wymagania wstępne

Aby ukończyć ten samouczek Szybki start, upewnij się, że dysponujesz następującymi elementami:

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]

- [Reguła zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla publicznego adresu IP komputera, który będzie używany w tym samouczku Szybki start.

- W systemie operacyjnym zainstalowano język Ruby i związane z nim oprogramowanie:
    - **System MacOS**: zainstaluj pakiet Homebrew, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS. Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **System Ubuntu**: zainstaluj oprogramowanie wymagane przez język Ruby, zainstaluj oprogramowanie rbenv i ruby-build, zainstaluj język Ruby, a następnie zainstaluj pakiet FreeTDS. Zobacz [kroki 1.2, 1.3 1.4 i 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Informacje o połączeniu z serwerem SQL

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]

> [!IMPORTANT]
> W przypadku publicznego adresu IP komputera, na którym jest wykonywany ten samouczek, niezbędne jest posiadanie reguły zapory. Jeśli pracujesz na innym komputerze lub masz inny publiczny adres IP, utwórz [regułę zapory poziomu serwera przy użyciu portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-to-query-sql-database"></a>Wstawianie kodu zapytania bazy danych SQL

1. W swoim ulubionym edytorze tekstów utwórz nowy plik o nazwie **sqltest.rb**

2. Zastąp jego zawartość następującym kodem i dodaj odpowiednie wartości dla serwera, bazy danych, użytkownika i hasła.

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

## <a name="run-the-code"></a>Uruchamianie kodu

1. W wierszu polecenia uruchom następujące polecenia:

   ```bash
   ruby sqltest.rb
   ```

2. Sprawdź, czy zostało zwróconych 20 pierwszych wierszy, a następnie zamknij okno aplikacji.


## <a name="next-steps"></a>Następne kroki
- [Projektowanie pierwszej bazy danych SQL na platformie Azure](sql-database-design-first-database.md)
- [Repozytorium GitHub dla rozwiązania TinyTDS](https://github.com/rails-sqlserver/tiny_tds)
- [Zgłoś problemy lub zadaj pytania dotyczące rozwiązania TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Sterowniki języka Ruby dla platformy SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
