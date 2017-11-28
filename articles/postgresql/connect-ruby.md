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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="1d633-103">Bazy danych platformy Azure dla PostgreSQL: Użyj Ruby danych tooconnect i zapytań</span><span class="sxs-lookup"><span data-stu-id="1d633-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="1d633-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych przy użyciu PostgreSQL [Ruby](https://www.ruby-lang.org) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d633-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="1d633-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="1d633-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="1d633-106">W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Ruby, ale, czy są nowe tooworking z bazą danych Azure dla PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d633-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1d633-107">Prerequisites</span></span>
<span data-ttu-id="1d633-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="1d633-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="1d633-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="1d633-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="1d633-110">Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d633-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="1d633-111">Instalowanie języka Ruby</span><span class="sxs-lookup"><span data-stu-id="1d633-111">Install Ruby</span></span>
<span data-ttu-id="1d633-112">Zainstaluj język Ruby na swojej maszynie.</span><span class="sxs-lookup"><span data-stu-id="1d633-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="1d633-113">Windows</span><span class="sxs-lookup"><span data-stu-id="1d633-113">Windows</span></span>
- <span data-ttu-id="1d633-114">Pobierz i zainstaluj hello najnowszej wersji [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1d633-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="1d633-115">Na powitania Zakończ ekranie powitania Instalator MSI, sprawdź pole hello "Uruchom"Zainstaluj ridk"tooinstall MSYS2 i łańcuch narzędzi rozwoju."</span><span class="sxs-lookup"><span data-stu-id="1d633-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="1d633-116">Następnie kliknij przycisk **Zakończ** toolaunch hello dalej Instalatora.</span><span class="sxs-lookup"><span data-stu-id="1d633-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="1d633-117">Uruchamia Instalator RubyInstaller2 dla systemu Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="1d633-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="1d633-118">Wpisz 2 tooinstall hello MSYS2 repozytorium aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1d633-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="1d633-119">Po zakończeniu i zwraca monit o zainstalowanie toohello, zamknij okno polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="1d633-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="1d633-120">Uruchamianie nowego wiersza polecenia (cmd) z hello Start menu.</span><span class="sxs-lookup"><span data-stu-id="1d633-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="1d633-121">Test hello dopisków fonetycznych instalacji `ruby -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1d633-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="1d633-122">Testowanie instalacji Gem hello `gem -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1d633-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="1d633-123">Utworzenie hello PostgreSQL modułu dla środowiska Ruby, używając polecenia hello Gem `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="1d633-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="1d633-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="1d633-124">MacOS</span></span>
- <span data-ttu-id="1d633-125">Instalowanie przy użyciu oprogramowania Homebrew, uruchamiając polecenie hello Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="1d633-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="1d633-126">Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="1d633-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="1d633-127">Test hello dopisków fonetycznych instalacji `ruby -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1d633-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="1d633-128">Testowanie instalacji Gem hello `gem -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1d633-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="1d633-129">Utworzenie hello PostgreSQL modułu dla środowiska Ruby, używając polecenia hello Gem `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="1d633-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="1d633-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="1d633-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="1d633-131">Zainstaluj Ruby, uruchamiając polecenie hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="1d633-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="1d633-132">Aby uzyskać więcej opcji instalacji, zobacz hello Ruby [dokumentacji instalacji](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="1d633-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="1d633-133">Test hello dopisków fonetycznych instalacji `ruby -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1d633-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="1d633-134">Zainstalować najnowsze aktualizacje hello Gem, uruchamiając polecenie hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="1d633-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="1d633-135">Testowanie instalacji Gem hello `gem -v` zainstalowanej wersji hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1d633-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="1d633-136">Zainstaluj hello gcc, marka i innych narzędzi do kompilacji, uruchamiając polecenie hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="1d633-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="1d633-137">Zainstaluj hello PostgreSQL biblioteki, uruchamiając polecenie hello `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="1d633-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="1d633-138">Utworzenie hello dopisków fonetycznych pg modułu przy użyciu Gem, uruchamiając polecenie hello `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="1d633-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="1d633-139">Uruchamianie kodu w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="1d633-139">Run Ruby code</span></span> 
- <span data-ttu-id="1d633-140">Zapisz hello kod do pliku tekstowego i Zapisz plik hello do folderu projektu z .rb rozszerzenia plików, takich jak `C:\rubypostgres\read.rb` lub`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="1d633-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="1d633-141">Kod hello toorun, uruchom wiersz polecenia hello lub powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="1d633-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="1d633-142">Zmień katalog na folder projektu `cd rubypostgres`, wpisz polecenie hello `ruby read.rb` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d633-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="1d633-143">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="1d633-143">Get connection information</span></span>
<span data-ttu-id="1d633-144">Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="1d633-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1d633-145">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="1d633-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="1d633-146">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1d633-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1d633-147">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="1d633-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="1d633-148">Kliknij nazwę serwera hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="1d633-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="1d633-149">Wybierz powitania serwera **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="1d633-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="1d633-150">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="1d633-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="1d633-151">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="1d633-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="1d633-152">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** nazwę logowania administratora serwera hello tooview strony.</span><span class="sxs-lookup"><span data-stu-id="1d633-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="1d633-153">W razie potrzeby Zresetuj hello hasło.</span><span class="sxs-lookup"><span data-stu-id="1d633-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="1d633-154">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="1d633-154">Connect and create a table</span></span>
<span data-ttu-id="1d633-155">Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="1d633-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="1d633-156">używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="1d633-157">A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) hello toorun polecenia UPUSZCZANIA, CREATE TABLE i INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="1d633-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="1d633-158">Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy.</span><span class="sxs-lookup"><span data-stu-id="1d633-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="1d633-159">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="1d633-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="1d633-160">Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="1d633-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="1d633-161">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="1d633-161">Read data</span></span>
<span data-ttu-id="1d633-162">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="1d633-163">używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="1d633-164">A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello wybierz polecenie utrzymywanie hello wyniki w zestawie wyników.</span><span class="sxs-lookup"><span data-stu-id="1d633-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="1d633-165">Witaj kolekcji zestawu wyników jest powtórzyć w przypadku hello `resultSet.each do` pętli zachowania hello bieżącej wartości wierszy w hello `row` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1d633-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="1d633-166">Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy.</span><span class="sxs-lookup"><span data-stu-id="1d633-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="1d633-167">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="1d633-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="1d633-168">Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="1d633-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="1d633-169">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="1d633-169">Update data</span></span>
<span data-ttu-id="1d633-170">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="1d633-171">używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="1d633-172">A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) hello toorun polecenia UPDATE.</span><span class="sxs-lookup"><span data-stu-id="1d633-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="1d633-173">Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy.</span><span class="sxs-lookup"><span data-stu-id="1d633-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="1d633-174">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="1d633-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="1d633-175">Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="1d633-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="1d633-176">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="1d633-176">Delete data</span></span>
<span data-ttu-id="1d633-177">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="1d633-178">używa kod Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) obiektów z konstruktorem [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooAzure tooconnect bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d633-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="1d633-179">A następnie wywołuje metodę [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) hello toorun polecenia UPDATE.</span><span class="sxs-lookup"><span data-stu-id="1d633-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="1d633-180">Witaj kodu sprawdza, czy błędy przy użyciu hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasy.</span><span class="sxs-lookup"><span data-stu-id="1d633-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="1d633-181">A następnie wywołuje metodę [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello połączenie przed przerwaniem.</span><span class="sxs-lookup"><span data-stu-id="1d633-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="1d633-182">Zastąp hello `host`, `database`, `user`, i `password` ciągów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="1d633-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="1d633-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d633-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1d633-184">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="1d633-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
