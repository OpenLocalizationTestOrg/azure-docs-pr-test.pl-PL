---
title: "tooAzure aaaConnect bazy danych przy użyciu Ruby PostgreSQL | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera przykładowy kod dopisków fonetycznych, można użyć tooconnect i wyszukiwać dane z bazy danych Azure PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla PostgreSQL: Użyj Ruby danych tooconnect i zapytań
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych przy użyciu PostgreSQL [Ruby](https://www.ruby-lang.org) aplikacji. Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Ruby, ale, czy są nowe tooworking z bazą danych Azure dla PostgreSQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie bazy danych — portal](quickstart-create-server-database-portal.md)
- [Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Instalowanie języka Ruby
Zainstaluj język Ruby na swojej maszynie. 

### <a name="windows"></a>Windows
- Pobierz i zainstaluj hello najnowszej wersji [Ruby](http://rubyinstaller.org/downloads/).
- Na powitania Zakończ ekranie powitania Instalator MSI, sprawdź pole hello "Uruchom"Zainstaluj ridk"tooinstall MSYS2 i łańcuch narzędzi rozwoju." Następnie kliknij przycisk **Zakończ** toolaunch hello dalej Instalatora.
- Uruchamia Instalator RubyInstaller2 dla systemu Windows Hello. Wpisz 2 tooinstall hello MSYS2 repozytorium aktualizacji. Po zakończeniu i zwraca monit o zainstalowanie toohello, zamknij okno polecenia hello.
- Uruchamianie nowego wiersza polecenia (cmd) z hello Start menu.
- Test hello dopisków fonetycznych instalacji `ruby -v` zainstalowanej wersji hello toosee.
- Testowanie instalacji Gem hello `gem -v` zainstalowanej wersji hello toosee.
- Utworzenie hello PostgreSQL modułu dla środowiska Ruby, używając polecenia hello Gem `gem install pg`.

### <a name="macos"></a>MacOS
- Instalowanie przy użyciu oprogramowania Homebrew, uruchamiając polecenie hello Ruby `brew install ruby`. Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Test hello dopisków fonetycznych instalacji `ruby -v` zainstalowanej wersji hello toosee.
- Testowanie instalacji Gem hello `gem -v` zainstalowanej wersji hello toosee.
- Utworzenie hello PostgreSQL modułu dla środowiska Ruby, używając polecenia hello Gem `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Zainstaluj Ruby, uruchamiając polecenie hello `sudo apt-get install ruby-full`. Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/).
- Test hello dopisków fonetycznych instalacji `ruby -v` zainstalowanej wersji hello toosee.
- Zainstalować najnowsze aktualizacje hello Gem, uruchamiając polecenie hello `sudo gem update --system`.
- Testowanie instalacji Gem hello `gem -v` zainstalowanej wersji hello toosee.
- Zainstaluj hello gcc, marka i innych narzędzi do kompilacji, uruchamiając polecenie hello `sudo apt-get install build-essential`.
- Zainstaluj hello PostgreSQL biblioteki, uruchamiając polecenie hello `sudo apt-get install libpq-dev`.
- Utworzenie hello dopisków fonetycznych pg modułu przy użyciu Gem, uruchamiając polecenie hello `sudo gem install pg`.

## <a name="run-ruby-code"></a>Uruchamianie kodu w języku Ruby 
- Zapisz hello kod do pliku tekstowego i Zapisz plik hello do folderu projektu z .rb rozszerzenia plików, takich jak `C:\rubypostgres\read.rb` lub`/home/username/rubypostgres/read.rb`
- Kod hello toorun, uruchom wiersz polecenia hello lub powłoki bash. Zmień katalog na folder projektu `cd rubypostgres`, wpisz polecenie hello `ruby read.rb` toorun hello aplikacji.

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **mypgserver 20170401**.
3. Kliknij nazwę serwera hello **mypgserver 20170401**.
4. Wybierz powitania serwera **omówienie** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-ruby/1-connection-string.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** nazwę logowania administratora serwera hello tooview strony. W razie potrzeby Zresetuj hello hasło.

## <a name="connect-and-create-a-table"></a>Łączenie i tworzenie tabeli
Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.

używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) hello toorun polecenia UPUSZCZANIA, CREATE TABLE i INSERT INTO. Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości. 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. 

używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello wybierz polecenie utrzymywanie hello wyniki w zestawie wyników. Witaj kolekcji zestawu wyników jest powtórzyć w przypadku hello `resultSet.each do` pętli zachowania hello bieżącej wartości wierszy w hello `row` zmiennej. Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.

używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) hello toorun polecenia UPDATE. Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. 

używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL. A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) hello toorun polecenia UPDATE. Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./howto-migrate-using-export-and-import.md)
