---
title: "Połącz tooAzure bazy danych dla PostgreSQL w języku Python | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera przykładowy kod języka Python można użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="5d471-103">Bazy danych platformy Azure dla PostgreSQL: Użyj Python tooconnect i zapytań danych</span><span class="sxs-lookup"><span data-stu-id="5d471-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="5d471-104">Ta opcja szybkiego startu przedstawia sposób toouse [Python](https://python.org) tooan tooconnect PostgreSQL bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5d471-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="5d471-105">Przedstawiono również sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello macOS, Ubuntu Linux i platform Windows.</span><span class="sxs-lookup"><span data-stu-id="5d471-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="5d471-106">Witaj opisanych w tym artykule założono, że znasz tworzenie przy użyciu języka Python i są nowe tooworking z bazą danych Azure dla PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="5d471-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d471-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5d471-107">Prerequisites</span></span>
<span data-ttu-id="5d471-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="5d471-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5d471-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="5d471-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="5d471-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5d471-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="5d471-111">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="5d471-111">You also need:</span></span>
- <span data-ttu-id="5d471-112">Zainstalowany język [python](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="5d471-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="5d471-113">Zainstalowany pakiet [pip](https://pip.pypa.io/en/stable/installing/) (pakiet pip jest już zainstalowany, jeśli używasz plików binarnych języka Python 2 w wersji 2.7.9 lub nowszej albo Python 3 w wersji 3.4 lub nowszej pobranych z witryny [python.org](https://python.org)).</span><span class="sxs-lookup"><span data-stu-id="5d471-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="5d471-114">Zainstaluj biblioteki połączeń hello języka Python dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5d471-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="5d471-115">Zainstaluj hello [psycopg2](http://initd.org/psycopg/docs/install.html) pakiet, który umożliwia tooconnect i zapytań hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d471-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="5d471-116">jest psycopg2 [dostępne na PyPI](https://pypi.python.org/pypi/psycopg2/) w formie hello [koło](http://pythonwheels.com/) pakietów hello najczęściej platform (z systemem Linux, OS x, Windows).</span><span class="sxs-lookup"><span data-stu-id="5d471-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="5d471-117">Użyj pip zainstalować tooget hello binarna wersja modułu hello wraz z zależnościami hello wszystkie.</span><span class="sxs-lookup"><span data-stu-id="5d471-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="5d471-118">Na komputerze uruchom interfejs wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="5d471-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="5d471-119">W systemie Linux Uruchom hello powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="5d471-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="5d471-120">Po macOS Uruchom hello terminalu.</span><span class="sxs-lookup"><span data-stu-id="5d471-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="5d471-121">W systemie Windows uruchom program hello wiersz polecenia z hello Start Menu.</span><span class="sxs-lookup"><span data-stu-id="5d471-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="5d471-122">Upewnij się, że używasz najnowszej wersji narzędzia pip hello za pomocą polecenia takie jak:</span><span class="sxs-lookup"><span data-stu-id="5d471-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="5d471-123">Uruchom następujące polecenie tooinstall hello psycopg2 pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="5d471-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="5d471-124">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="5d471-124">Get connection information</span></span>
<span data-ttu-id="5d471-125">Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5d471-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="5d471-126">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="5d471-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5d471-127">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5d471-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5d471-128">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj **mypgserver 20170401** (serwer hello właśnie utworzony).</span><span class="sxs-lookup"><span data-stu-id="5d471-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="5d471-129">Kliknij nazwę serwera hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="5d471-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="5d471-130">Wybierz powitania serwera **omówienie** strony, a następnie zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="5d471-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5d471-131">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="5d471-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="5d471-132">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="5d471-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="5d471-133">Jak toorun kodu języka Python</span><span class="sxs-lookup"><span data-stu-id="5d471-133">How toorun Python code</span></span>
<span data-ttu-id="5d471-134">Ten temat zawiera łącznie cztery przykłady kodu, z których każdy wykonuje konkretną funkcję.</span><span class="sxs-lookup"><span data-stu-id="5d471-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="5d471-135">Witaj poniższe instrukcje wskazują sposób Wstaw blok kodu toocreate pliku tekstowego, a następnie zapisz plik hello, tak, aby uruchomić ją później.</span><span class="sxs-lookup"><span data-stu-id="5d471-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="5d471-136">Należy się toocreate czterech oddzielnych plików, po jednej dla każdego bloku kodu.</span><span class="sxs-lookup"><span data-stu-id="5d471-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="5d471-137">W swoim ulubionym edytorze tekstów utwórz nowy plik.</span><span class="sxs-lookup"><span data-stu-id="5d471-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="5d471-138">Skopiuj i Wklej jedną z próbek kodu hello w hello następujące sekcje w pliku tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="5d471-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="5d471-139">Zastąp hello **hosta**, **dbname**, **użytkownika**, i **hasło** parametry z wartościami hello określone podczas tworzenia hello serwer i bazę danych.</span><span class="sxs-lookup"><span data-stu-id="5d471-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="5d471-140">Zapisz hello plik z rozszerzeniem .py hello (na przykład postgres.py) w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="5d471-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="5d471-141">Jeśli korzystasz z systemu operacyjnego Windows hello, należy się tooselect kodowania UTF-8 podczas zapisywania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="5d471-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="5d471-142">Uruchom powłokę wiersza polecenia lub Bash hello, a następnie zmień folder tooyour hello katalogu projektu, na przykład `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="5d471-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="5d471-143">Kod hello toorun, hello typ polecenia języka Python, następuje hello nazwę pliku, na przykład `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="5d471-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="5d471-144">Począwszy od języka Python w wersji 3, może zostać wyświetlony błąd hello `SyntaxError: Missing parentheses in call too'print'` podczas uruchamiania powitania po bloków kodu.</span><span class="sxs-lookup"><span data-stu-id="5d471-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="5d471-145">Jeśli tak się stanie, Zastąp każde polecenie toohello wywołania `print "string"` z wywołania funkcji przy użyciu nawias, takich jak `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="5d471-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5d471-146">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="5d471-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="5d471-147">Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) działać z **Wstaw** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5d471-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="5d471-148">Witaj [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="5d471-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="5d471-149">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d471-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="5d471-150">Po hello kodu zostanie wykonane pomyślnie, dane wyjściowe hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="5d471-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Dane wyjściowe wiersza polecenia](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="5d471-152">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="5d471-152">Read data</span></span>
<span data-ttu-id="5d471-153">Użyj hello poniższy kod tooread hello danych za pomocą [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) działać z **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5d471-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="5d471-154">Ta funkcja akceptuje zapytania i zwraca zestawu wyników, które można powtórzyć za pośrednictwem z użyciem hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="5d471-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="5d471-155">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d471-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="5d471-156">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="5d471-156">Update data</span></span>
<span data-ttu-id="5d471-157">Użyj hello poniższy kod tooupdate hello spisu wiersza, który został wcześniej wstawiony przy użyciu [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) działać z **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5d471-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="5d471-158">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d471-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="5d471-159">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="5d471-159">Delete data</span></span>
<span data-ttu-id="5d471-160">Użyj hello poniższy kod toodelete elementu spisu, który wcześniej wstawiony przy użyciu [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) działać z **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5d471-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="5d471-161">Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d471-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="5d471-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d471-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5d471-163">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="5d471-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
