---
title: "Nawiązywanie połączeń z usługą Azure Database for MySQL za pomocą języka Ruby | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera kilka przykładów kodu języka Ruby, których można używać do nawiązywania połączeń z danymi usługi Azure Database for MySQL i wykonywania zapytań względem nich."
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
ms.openlocfilehash: e54f1dccbae060c52f48bfeb277c045b99a91715
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="4bdce-103">Usługa Azure Database for MySQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą języka Ruby</span><span class="sxs-lookup"><span data-stu-id="4bdce-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="4bdce-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for MySQL przy użyciu aplikacji języka [Ruby](https://www.ruby-lang.org) i rozwiązania gem [mysql2](https://rubygems.org/gems/mysql2) na platformach Windows, Ubuntu Linux i Mac.</span><span class="sxs-lookup"><span data-stu-id="4bdce-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="4bdce-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="4bdce-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="4bdce-106">W tym artykule założono, że wiesz już, jak programować za pomocą języka Ruby, i dopiero zaczynasz pracę z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bdce-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4bdce-107">Prerequisites</span></span>
<span data-ttu-id="4bdce-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="4bdce-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4bdce-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4bdce-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4bdce-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4bdce-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="4bdce-111">Instalowanie języka Ruby</span><span class="sxs-lookup"><span data-stu-id="4bdce-111">Install Ruby</span></span>
<span data-ttu-id="4bdce-112">Zainstaluj język Ruby, rozwiązanie Gem i bibliotekę MySQL2 na własnej maszynie.</span><span class="sxs-lookup"><span data-stu-id="4bdce-112">Install Ruby, Gem, and the MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="4bdce-113">Windows</span><span class="sxs-lookup"><span data-stu-id="4bdce-113">Windows</span></span>
1. <span data-ttu-id="4bdce-114">Pobierz i zainstaluj wersję 2.3 języka [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4bdce-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="4bdce-115">Uruchom nowy wiersz polecenia (cmd) z menu Start.</span><span class="sxs-lookup"><span data-stu-id="4bdce-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="4bdce-116">Zmień katalog na katalog języka Ruby w wersji 2.3.</span><span class="sxs-lookup"><span data-stu-id="4bdce-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="4bdce-117">Przetestuj instalację języka Ruby, uruchamiając polecenie `ruby -v`, aby sprawdzić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="4bdce-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="4bdce-118">Przetestuj instalację rozwiązania Gem, uruchamiając polecenie `gem -v`, aby sprawdzić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="4bdce-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="4bdce-119">Skompiluj moduł Mysql2 dla języka Ruby przy użyciu rozwiązania Gem, uruchamiając polecenie `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="4bdce-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="4bdce-120">MacOS</span></span>
1. <span data-ttu-id="4bdce-121">Zainstaluj język Ruby przy użyciu programu Homebrew, uruchamiając polecenie `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="4bdce-122">Informacje na temat kolejnych opcji instalacji można znaleźć w [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/#homebrew) języka Ruby.</span><span class="sxs-lookup"><span data-stu-id="4bdce-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="4bdce-123">Przetestuj instalację języka Ruby, uruchamiając polecenie `ruby -v`, aby sprawdzić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="4bdce-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="4bdce-124">Przetestuj instalację rozwiązania Gem, uruchamiając polecenie `gem -v`, aby sprawdzić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="4bdce-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="4bdce-125">Skompiluj moduł Mysql2 dla języka Ruby przy użyciu rozwiązania Gem, uruchamiając polecenie `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4bdce-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4bdce-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="4bdce-127">Zainstaluj język Ruby, uruchamiając polecenie `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="4bdce-128">Informacje na temat kolejnych opcji instalacji można znaleźć w [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/) języka Ruby.</span><span class="sxs-lookup"><span data-stu-id="4bdce-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="4bdce-129">Przetestuj instalację języka Ruby, uruchamiając polecenie `ruby -v`, aby sprawdzić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="4bdce-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="4bdce-130">Zainstaluj najnowsze aktualizacje rozwiązania Gem, uruchamiając polecenie `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="4bdce-131">Przetestuj instalację rozwiązania Gem, uruchamiając polecenie `gem -v`, aby sprawdzić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="4bdce-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="4bdce-132">Zainstaluj narzędzia gcc, make i inne narzędzia do kompilacji, uruchamiając polecenie `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="4bdce-133">Zainstaluj biblioteki klienckie dewelopera programu MySQL, uruchamiając polecenie `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="4bdce-134">Skompiluj moduł mysql2 dla języka Ruby przy użyciu rozwiązania Gem, uruchamiając polecenie `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4bdce-135">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="4bdce-135">Get connection information</span></span>
<span data-ttu-id="4bdce-136">Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="4bdce-137">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="4bdce-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4bdce-138">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4bdce-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4bdce-139">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="4bdce-139">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="4bdce-140">Kliknij nazwę serwera **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="4bdce-140">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="4bdce-141">Wybierz stronę **Właściwości** serwera.</span><span class="sxs-lookup"><span data-stu-id="4bdce-141">Select the server's **Properties** page.</span></span> <span data-ttu-id="4bdce-142">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="4bdce-142">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4bdce-143">![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4bdce-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4bdce-144">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="4bdce-144">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="4bdce-145">Uruchamianie kodu w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="4bdce-145">Run Ruby code</span></span> 
1. <span data-ttu-id="4bdce-146">Wklej kod języka Ruby z sekcji poniżej do plików tekstowych i zapisz pliki w folderze projektu z rozszerzeniem pliku rb, takim jak `C:\rubymysql\createtable.rb` lub `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="4bdce-146">Paste the Ruby code from the sections below into text files, and save the files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="4bdce-147">Aby uruchomić kod, uruchom wiersz polecenia lub powłokę bash.</span><span class="sxs-lookup"><span data-stu-id="4bdce-147">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="4bdce-148">Zmień katalog na folder projektu `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="4bdce-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="4bdce-149">Następnie wpisz polecenie ruby, a po nim nazwę pliku, taką jak `ruby createtable.rb`, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="4bdce-149">Then type the ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="4bdce-150">W systemie Windows, jeśli aplikacja języka Ruby nie znajduje się w zmiennej środowiskowej path, może być konieczne użycie pełnej ścieżki w celu uruchomienia aplikacji Node, takiej jak `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="4bdce-150">On the Windows OS, if the ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="4bdce-151">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="4bdce-151">Connect and create a table</span></span>
<span data-ttu-id="4bdce-152">Użyj poniższego kodu w celu nawiązania połączenia i utworzenia tabeli za pomocą instrukcji **CREATE TABLE** języka SQL, a następnie instrukcji **INSERT INTO** języka SQL, aby dodać wiersze do tabeli.</span><span class="sxs-lookup"><span data-stu-id="4bdce-152">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="4bdce-153">Kod używa metody .new() klasy [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) w celu nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-153">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="4bdce-154">Następnie kilka razy wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) w celu uruchomienia poleceń DROP, CREATE TABLE i INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="4bdce-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="4bdce-155">W kolejnym kroku kod wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) w celu zamknięcia połączenia przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="4bdce-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="4bdce-156">Zastąp ciągi `host`, `database`, `username` i `password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="4bdce-156">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection to database.'

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

## <a name="read-data"></a><span data-ttu-id="4bdce-157">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="4bdce-157">Read data</span></span>
<span data-ttu-id="4bdce-158">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-158">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="4bdce-159">Kod używa metody .new() klasy [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) w celu nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-159">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="4bdce-160">Następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) w celu uruchomienia poleceń SELECT.</span><span class="sxs-lookup"><span data-stu-id="4bdce-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="4bdce-161">W kolejnym kroku kod wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) w celu zamknięcia połączenia przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="4bdce-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="4bdce-162">Zastąp ciągi `host`, `database`, `username` i `password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="4bdce-162">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="update-data"></a><span data-ttu-id="4bdce-163">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="4bdce-163">Update data</span></span>
<span data-ttu-id="4bdce-164">Użyj poniższego kodu, aby nawiązać połączenie i zaktualizować dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-164">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="4bdce-165">Kod używa metody .new() klasy [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) w celu nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-165">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="4bdce-166">Następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) w celu uruchomienia poleceń UPDATE.</span><span class="sxs-lookup"><span data-stu-id="4bdce-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="4bdce-167">W kolejnym kroku kod wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) w celu zamknięcia połączenia przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="4bdce-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="4bdce-168">Zastąp ciągi `host`, `database`, `username` i `password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="4bdce-168">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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


## <a name="delete-data"></a><span data-ttu-id="4bdce-169">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="4bdce-169">Delete data</span></span>
<span data-ttu-id="4bdce-170">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-170">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4bdce-171">Kod używa metody .new() klasy [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) w celu nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bdce-171">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="4bdce-172">Następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) w celu uruchomienia poleceń DELETE.</span><span class="sxs-lookup"><span data-stu-id="4bdce-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="4bdce-173">W kolejnym kroku kod wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) w celu zamknięcia połączenia przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="4bdce-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="4bdce-174">Zastąp ciągi `host`, `database`, `username` i `password` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="4bdce-174">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="next-steps"></a><span data-ttu-id="4bdce-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4bdce-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4bdce-176">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="4bdce-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
