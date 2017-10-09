---
title: "Połącz tooAzure bazy danych dla programu MySQL w języku Python | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera kilka Python code przykłady korzystania tooconnect i zapytań dane z bazy danych Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="496e7-103">Bazy danych platformy Azure dla programu MySQL: Użyj Python tooconnect i zapytań danych</span><span class="sxs-lookup"><span data-stu-id="496e7-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="496e7-104">Ta opcja szybkiego startu przedstawia sposób toouse [Python](https://python.org) tooan tooconnect bazy danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="496e7-105">Używa tooquery instrukcji SQL, wstawiania, aktualizacji i usuwania danych w bazie danych hello z platform systemu Mac OS, Ubuntu Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="496e7-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="496e7-106">Witaj opisanych w tym artykule założono, że znasz tworzenie przy użyciu języka Python i są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="496e7-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="496e7-107">Prerequisites</span></span>
<span data-ttu-id="496e7-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="496e7-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="496e7-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="496e7-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="496e7-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="496e7-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="496e7-111">Instalowanie języka Python i hello MySQL łącznika</span><span class="sxs-lookup"><span data-stu-id="496e7-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="496e7-112">Zainstaluj [Python](https://www.python.org/downloads/) i hello [łącznika MySQL dla języka Python](https://dev.mysql.com/downloads/connector/python/) na własnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="496e7-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="496e7-113">W zależności od platformy wykonaj kroki hello:</span><span class="sxs-lookup"><span data-stu-id="496e7-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="496e7-114">Windows</span><span class="sxs-lookup"><span data-stu-id="496e7-114">Windows</span></span>
1. <span data-ttu-id="496e7-115">Pobierz i zainstaluj język Python w wersji 2.7 z witryny [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="496e7-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="496e7-116">Sprawdź hello instalacji języka Python, uruchamiając wiersz polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="496e7-117">Uruchom polecenie hello `C:\python27\python.exe -V` przy użyciu hello wielkie V przełącznika toosee hello numer wersji.</span><span class="sxs-lookup"><span data-stu-id="496e7-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="496e7-118">Zainstaluj hello Python łącznik dla programu MySQL z [mysql.com](https://dev.mysql.com/downloads/connector/python/) tooyour odpowiedniej wersji języka Python.</span><span class="sxs-lookup"><span data-stu-id="496e7-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="496e7-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="496e7-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="496e7-120">W systemie Linux (Ubuntu) Python jest instalowane jako część hello domyślnej instalacji.</span><span class="sxs-lookup"><span data-stu-id="496e7-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="496e7-121">Uruchamianie powłoki bash hello Sprawdź hello instalacji języka Python.</span><span class="sxs-lookup"><span data-stu-id="496e7-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="496e7-122">Uruchom polecenie hello `python -V` przy użyciu hello wielkie V przełącznika toosee hello numer wersji.</span><span class="sxs-lookup"><span data-stu-id="496e7-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="496e7-123">Sprawdź hello instalacji narzędzia PIP, uruchamiając hello `pip show pip -V` numer wersji hello toosee polecenia.</span><span class="sxs-lookup"><span data-stu-id="496e7-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="496e7-124">Narzędzie PIP może być dołączone w niektórych wersjach środowiska Python.</span><span class="sxs-lookup"><span data-stu-id="496e7-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="496e7-125">Jeśli nie zainstalowano narzędzia PIP, można zainstalować hello [PIP] (https://pip.pypa.io/en/stable/installing/) pakietu, uruchamiając polecenie `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="496e7-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="496e7-126">Aktualizacja adresu PIP toohello najnowszej wersji, uruchamiając hello `pip install -U pip` polecenia.</span><span class="sxs-lookup"><span data-stu-id="496e7-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="496e7-127">Zainstalować łącznik MySQL hello Python i jego zależności za pomocą polecenia PIP hello:</span><span class="sxs-lookup"><span data-stu-id="496e7-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="496e7-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="496e7-128">MacOS</span></span>
1. <span data-ttu-id="496e7-129">W systemie Mac OS Python jest instalowane jako część hello domyślna instalacja systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="496e7-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="496e7-130">Uruchamianie powłoki bash hello Sprawdź hello instalacji języka Python.</span><span class="sxs-lookup"><span data-stu-id="496e7-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="496e7-131">Uruchom polecenie hello `python -V` przy użyciu hello wielkie V przełącznika toosee hello numer wersji.</span><span class="sxs-lookup"><span data-stu-id="496e7-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="496e7-132">Sprawdź hello instalacji narzędzia PIP, uruchamiając hello `pip show pip -V` numer wersji hello toosee polecenia.</span><span class="sxs-lookup"><span data-stu-id="496e7-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="496e7-133">Narzędzie PIP może być dołączone w niektórych wersjach środowiska Python.</span><span class="sxs-lookup"><span data-stu-id="496e7-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="496e7-134">Jeśli nie zainstalowano narzędzia PIP, można zainstalować hello [PIP](https://pip.pypa.io/en/stable/installing/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="496e7-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="496e7-135">Aktualizacja adresu PIP toohello najnowszej wersji, uruchamiając hello `pip install -U pip` polecenia.</span><span class="sxs-lookup"><span data-stu-id="496e7-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="496e7-136">Zainstalować łącznik MySQL hello Python i jego zależności za pomocą polecenia PIP hello:</span><span class="sxs-lookup"><span data-stu-id="496e7-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="496e7-137">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="496e7-137">Get connection information</span></span>
<span data-ttu-id="496e7-138">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="496e7-139">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="496e7-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="496e7-140">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="496e7-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="496e7-141">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj hello serwera, musisz mieć wydłużało, takich jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="496e7-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="496e7-142">Kliknij nazwę serwera hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="496e7-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="496e7-143">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="496e7-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="496e7-144">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="496e7-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="496e7-145">![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="496e7-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="496e7-146">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="496e7-147">Uruchamianie kodu języka Python</span><span class="sxs-lookup"><span data-stu-id="496e7-147">Run Python Code</span></span>
- <span data-ttu-id="496e7-148">Wklej hello kod do pliku tekstowego, a następnie zapisz plik hello do folderu projektu z PY i rozszerzenia plików, na przykład C:\pythonmysql\createtable.py lub /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="496e7-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="496e7-149">Kod hello toorun, uruchom wiersz polecenia hello lub powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="496e7-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="496e7-150">Zmień katalog na folder projektu `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="496e7-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="496e7-151">Następnie wpisz polecenie python hello następuje nazwa pliku hello `python createtable.py` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="496e7-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="496e7-152">Na powitania systemu operacyjnego Windows Jeśli python.exe nie zostanie znaleziony, możesz podać hello — toohello Pełna ścieżka pliku wykonywalnego lub Dodaj hello Python ścieżki do zmiennej środowiskowej path hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="496e7-153">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="496e7-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="496e7-154">Użyj następujących hello kodu serwera toohello tooconnect, Utwórz tabelę i załadować hello danych przy użyciu **Wstaw** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="496e7-155">W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="496e7-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="496e7-156">Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="496e7-157">Kod Hello korzysta z kursora hello połączenia i i [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje zapytanie SQL hello w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="496e7-158">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="496e7-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a><span data-ttu-id="496e7-159">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="496e7-159">Read data</span></span>
<span data-ttu-id="496e7-160">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="496e7-161">W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="496e7-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="496e7-162">Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="496e7-163">Kod Hello korzysta z kursora na powitania połączenia, a [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje instrukcję SQL hello w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="496e7-164">wiersze danych Hello są odczytywane przy użyciu hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) metody.</span><span class="sxs-lookup"><span data-stu-id="496e7-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="496e7-165">Witaj zestaw wyników jest przechowywany w kolekcji wiersza i iteratora jest tooloop używanych przez hello wierszy.</span><span class="sxs-lookup"><span data-stu-id="496e7-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="496e7-166">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="496e7-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a><span data-ttu-id="496e7-167">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="496e7-167">Update data</span></span>
<span data-ttu-id="496e7-168">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="496e7-169">W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="496e7-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="496e7-170">Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="496e7-171">Kod Hello korzysta z kursora na powitania połączenia, a [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje instrukcję SQL hello w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="496e7-172">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="496e7-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="496e7-173">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="496e7-173">Delete data</span></span>
<span data-ttu-id="496e7-174">Użyj hello następujący kod tooconnect i usuwanie danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="496e7-175">W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="496e7-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="496e7-176">Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello.</span><span class="sxs-lookup"><span data-stu-id="496e7-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="496e7-177">Kod Hello korzysta z kursora hello połączenia i i [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje zapytanie SQL hello w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="496e7-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="496e7-178">Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="496e7-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="496e7-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="496e7-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="496e7-180">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="496e7-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
