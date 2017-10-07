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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="af53a-103">Bazy danych platformy Azure dla programu MySQL: Użyj Ruby danych tooconnect i zapytań</span><span class="sxs-lookup"><span data-stu-id="af53a-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="af53a-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu [Ruby](https://www.ruby-lang.org) aplikacji i hello [mysql2](https://rubygems.org/gems/mysql2) gem z systemu Windows, Ubuntu Linux i komputerów Mac platform.</span><span class="sxs-lookup"><span data-stu-id="af53a-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="af53a-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="af53a-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="af53a-106">W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Ruby, ale, czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af53a-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af53a-107">Prerequisites</span></span>
<span data-ttu-id="af53a-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="af53a-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="af53a-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="af53a-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="af53a-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="af53a-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="af53a-111">Instalowanie języka Ruby</span><span class="sxs-lookup"><span data-stu-id="af53a-111">Install Ruby</span></span>
<span data-ttu-id="af53a-112">Zainstaluj Ruby, Gem i biblioteki MySQL2 hello na własnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="af53a-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="af53a-113">Windows</span><span class="sxs-lookup"><span data-stu-id="af53a-113">Windows</span></span>
1. <span data-ttu-id="af53a-114">Pobierz i zainstaluj hello 2.3 wersji [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="af53a-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="af53a-115">Uruchamianie nowego wiersza polecenia (cmd) z hello Start menu.</span><span class="sxs-lookup"><span data-stu-id="af53a-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="af53a-116">Zmień katalog na powitania katalogu dopisków fonetycznych dla wersji 2.3.</span><span class="sxs-lookup"><span data-stu-id="af53a-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="af53a-117">Test hello dopisków fonetycznych instalacji przez uruchomienie polecenia hello `ruby -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="af53a-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="af53a-118">Testowanie instalacji Gem hello, uruchamiając polecenie hello `gem -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="af53a-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="af53a-119">Utworzenie modułu hello Mysql2 dla środowiska Ruby, używając polecenia hello Gem `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="af53a-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="af53a-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="af53a-120">MacOS</span></span>
1. <span data-ttu-id="af53a-121">Instalowanie przy użyciu oprogramowania Homebrew, uruchamiając polecenie hello Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="af53a-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="af53a-122">Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="af53a-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="af53a-123">Test hello dopisków fonetycznych instalacji przez uruchomienie polecenia hello `ruby -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="af53a-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="af53a-124">Testowanie instalacji Gem hello, uruchamiając polecenie hello `gem -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="af53a-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="af53a-125">Utworzenie modułu hello Mysql2 dla środowiska Ruby, używając polecenia hello Gem `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="af53a-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="af53a-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="af53a-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="af53a-127">Zainstaluj Ruby, uruchamiając polecenie hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="af53a-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="af53a-128">Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="af53a-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="af53a-129">Test hello dopisków fonetycznych instalacji przez uruchomienie polecenia hello `ruby -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="af53a-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="af53a-130">Zainstalować najnowsze aktualizacje hello Gem, uruchamiając polecenie hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="af53a-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="af53a-131">Testowanie instalacji Gem hello, uruchamiając polecenie hello `gem -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="af53a-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="af53a-132">Zainstaluj hello gcc, marka i innych narzędzi do kompilacji, uruchamiając polecenie hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="af53a-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="af53a-133">Zainstaluj bibliotek developer klienta MySQL hello, uruchamiając polecenie hello `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="af53a-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="af53a-134">Utworzenie hello mysql2 modułu dla środowiska Ruby, używając polecenia hello Gem `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="af53a-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="af53a-135">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="af53a-135">Get connection information</span></span>
<span data-ttu-id="af53a-136">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="af53a-137">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="af53a-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="af53a-138">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="af53a-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="af53a-139">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj hello serwera, musisz mieć wydłużało, takich jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="af53a-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="af53a-140">Kliknij nazwę serwera hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="af53a-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="af53a-141">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="af53a-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="af53a-142">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="af53a-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="af53a-143">![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="af53a-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="af53a-144">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="af53a-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="af53a-145">Uruchamianie kodu w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="af53a-145">Run Ruby code</span></span> 
1. <span data-ttu-id="af53a-146">Wklej hello dopisków fonetycznych kod z sekcjami hello do plików tekstowych i zapisywać pliki hello do folderu projektu z .rb rozszerzenia plików, takich jak `C:\rubymysql\createtable.rb` lub `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="af53a-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="af53a-147">Kod hello toorun, uruchom wiersz polecenia hello lub powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="af53a-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="af53a-148">Zmień katalog na folder projektu `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="af53a-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="af53a-149">Następnie wpisz polecenie hello dopisków fonetycznych następuje nazwa pliku hello, takich jak `ruby createtable.rb` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af53a-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="af53a-150">Na powitania systemu operacyjnego Windows aplikacji hello dopisków fonetycznych nie znajduje się w sieci zmiennej środowiskowej path, konieczne może toouse hello pełną ścieżkę toolaunch hello węzła aplikacji, takich jak`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="af53a-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="af53a-151">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="af53a-151">Connect and create a table</span></span>
<span data-ttu-id="af53a-152">Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="af53a-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="af53a-153">używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="af53a-154">A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) kilka razy toorun hello UPUSZCZANIA, CREATE TABLE i INSERT INTO poleceń.</span><span class="sxs-lookup"><span data-stu-id="af53a-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="af53a-155">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="af53a-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="af53a-156">Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="af53a-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="af53a-157">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="af53a-157">Read data</span></span>
<span data-ttu-id="af53a-158">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="af53a-159">używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="af53a-160">A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello wybierz polecenia.</span><span class="sxs-lookup"><span data-stu-id="af53a-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="af53a-161">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="af53a-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="af53a-162">Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="af53a-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="af53a-163">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="af53a-163">Update data</span></span>
<span data-ttu-id="af53a-164">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="af53a-165">używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="af53a-166">A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello aktualizacji poleceń.</span><span class="sxs-lookup"><span data-stu-id="af53a-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="af53a-167">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="af53a-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="af53a-168">Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="af53a-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="af53a-169">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="af53a-169">Delete data</span></span>
<span data-ttu-id="af53a-170">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="af53a-171">używa kod Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) klasy .new() metody tooconnect tooAzure bazy danych dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="af53a-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="af53a-172">A następnie wywołuje metodę [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE poleceń.</span><span class="sxs-lookup"><span data-stu-id="af53a-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="af53a-173">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="af53a-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="af53a-174">Zastąp hello `host`, `database`, `username`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="af53a-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="af53a-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af53a-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="af53a-176">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="af53a-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
