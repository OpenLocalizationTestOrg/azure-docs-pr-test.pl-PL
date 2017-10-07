---
title: "Połącz tooAzure bazy danych dla programu MySQL przy użyciu Ruby | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera kilka przykładów kodu dopisków fonetycznych, można użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: Użyj Ruby danych tooconnect i zapytań
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu [Ruby](https://www.ruby-lang.org) aplikacji i hello [mysql2](https://rubygems.org/gems/mysql2) gem z systemu Windows, Ubuntu Linux i komputerów Mac platform. Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Ruby, ale, czy są nowe tooworking z bazą danych Azure dla programu MySQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a>Instalowanie języka Ruby
Zainstaluj Ruby, Gem i biblioteki MySQL2 hello na własnym komputerze. 

### <a name="windows"></a>Windows
1. Pobierz i zainstaluj hello 2.3 wersji [Ruby](http://rubyinstaller.org/downloads/).
2. Uruchamianie nowego wiersza polecenia (cmd) z hello Start menu.
3. Zmień katalog na powitania katalogu dopisków fonetycznych dla wersji 2.3. `cd c:\Ruby23-x64\bin`
4. Test hello dopisków fonetycznych instalacji przez uruchomienie polecenia hello `ruby -v` zainstalowanej wersji hello toosee.
5. Testowanie instalacji Gem hello, uruchamiając polecenie hello `gem -v` zainstalowanej wersji hello toosee.
6. Utworzenie modułu hello Mysql2 dla środowiska Ruby, używając polecenia hello Gem `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Instalowanie przy użyciu oprogramowania Homebrew, uruchamiając polecenie hello Ruby `brew install ruby`. Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Test hello dopisków fonetycznych instalacji przez uruchomienie polecenia hello `ruby -v` zainstalowanej wersji hello toosee.
3. Testowanie instalacji Gem hello, uruchamiając polecenie hello `gem -v` zainstalowanej wersji hello toosee.
4. Utworzenie modułu hello Mysql2 dla środowiska Ruby, używając polecenia hello Gem `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Zainstaluj Ruby, uruchamiając polecenie hello `sudo apt-get install ruby-full`. Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/).
2. Test hello dopisków fonetycznych instalacji przez uruchomienie polecenia hello `ruby -v` zainstalowanej wersji hello toosee.
3. Zainstalować najnowsze aktualizacje hello Gem, uruchamiając polecenie hello `sudo gem update --system`.
4. Testowanie instalacji Gem hello, uruchamiając polecenie hello `gem -v` zainstalowanej wersji hello toosee.
5. Zainstaluj hello gcc, marka i innych narzędzi do kompilacji, uruchamiając polecenie hello `sudo apt-get install build-essential`.
6. Zainstaluj bibliotek developer klienta MySQL hello, uruchamiając polecenie hello `sudo apt-get install libmysqlclient-dev`.
7. Utworzenie hello mysql2 modułu dla środowiska Ruby, używając polecenia hello Gem `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj hello serwera, musisz mieć wydłużało, takich jak **myserver4demo**.
3. Kliknij nazwę serwera hello **myserver4demo**.
4. Wybierz powitania serwera **właściwości** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-ruby/1_server-properties-name-login.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="run-ruby-code"></a>Uruchamianie kodu w języku Ruby 
1. Wklej hello dopisków fonetycznych kod z sekcjami hello do plików tekstowych i zapisywać pliki hello do folderu projektu z .rb rozszerzenia plików, takich jak `C:\rubymysql\createtable.rb` lub `/home/username/rubymysql/createtable.rb`.
2. Kod hello toorun, uruchom wiersz polecenia hello lub powłoki bash. Zmień katalog na folder projektu `cd rubymysql`
3. Następnie wpisz polecenie hello dopisków fonetycznych następuje nazwa pliku hello, takich jak `ruby createtable.rb` toorun hello aplikacji.
4. Na powitania systemu operacyjnego Windows aplikacji hello dopisków fonetycznych nie znajduje się w sieci zmiennej środowiskowej path, konieczne może toouse hello pełną ścieżkę toolaunch hello węzła aplikacji, takich jak`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Łączenie i tworzenie tabeli
Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.

używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL. A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) kilka razy toorun hello UPUSZCZANIA, CREATE TABLE i INSERT INTO poleceń. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości. 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. 

używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL. A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello wybierz polecenia. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.

używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL. A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello aktualizacji poleceń. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. 

używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL. A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE poleceń. A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.

Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./concepts-migrate-import-export.md)
