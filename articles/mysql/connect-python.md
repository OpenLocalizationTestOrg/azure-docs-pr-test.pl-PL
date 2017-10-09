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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: Użyj Python tooconnect i zapytań danych
Ta opcja szybkiego startu przedstawia sposób toouse [Python](https://python.org) tooan tooconnect bazy danych Azure dla programu MySQL. Używa tooquery instrukcji SQL, wstawiania, aktualizacji i usuwania danych w bazie danych hello z platform systemu Mac OS, Ubuntu Linux i Windows. Witaj opisanych w tym artykule założono, że znasz tworzenie przy użyciu języka Python i są nowe tooworking z bazą danych Azure dla programu MySQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>Instalowanie języka Python i hello MySQL łącznika
Zainstaluj [Python](https://www.python.org/downloads/) i hello [łącznika MySQL dla języka Python](https://dev.mysql.com/downloads/connector/python/) na własnym komputerze. W zależności od platformy wykonaj kroki hello:

### <a name="windows"></a>Windows
1. Pobierz i zainstaluj język Python w wersji 2.7 z witryny [python.org](https://www.python.org/downloads/windows/). 
2. Sprawdź hello instalacji języka Python, uruchamiając wiersz polecenia hello. Uruchom polecenie hello `C:\python27\python.exe -V` przy użyciu hello wielkie V przełącznika toosee hello numer wersji.
3. Zainstaluj hello Python łącznik dla programu MySQL z [mysql.com](https://dev.mysql.com/downloads/connector/python/) tooyour odpowiedniej wersji języka Python.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. W systemie Linux (Ubuntu) Python jest instalowane jako część hello domyślnej instalacji.
2. Uruchamianie powłoki bash hello Sprawdź hello instalacji języka Python. Uruchom polecenie hello `python -V` przy użyciu hello wielkie V przełącznika toosee hello numer wersji.
3. Sprawdź hello instalacji narzędzia PIP, uruchamiając hello `pip show pip -V` numer wersji hello toosee polecenia. 
4. Narzędzie PIP może być dołączone w niektórych wersjach środowiska Python. Jeśli nie zainstalowano narzędzia PIP, można zainstalować hello [PIP] (https://pip.pypa.io/en/stable/installing/) pakietu, uruchamiając polecenie `sudo apt-get install python-pip`.
5. Aktualizacja adresu PIP toohello najnowszej wersji, uruchamiając hello `pip install -U pip` polecenia.
6. Zainstalować łącznik MySQL hello Python i jego zależności za pomocą polecenia PIP hello:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. W systemie Mac OS Python jest instalowane jako część hello domyślna instalacja systemu operacyjnego.
2. Uruchamianie powłoki bash hello Sprawdź hello instalacji języka Python. Uruchom polecenie hello `python -V` przy użyciu hello wielkie V przełącznika toosee hello numer wersji.
3. Sprawdź hello instalacji narzędzia PIP, uruchamiając hello `pip show pip -V` numer wersji hello toosee polecenia.
4. Narzędzie PIP może być dołączone w niektórych wersjach środowiska Python. Jeśli nie zainstalowano narzędzia PIP, można zainstalować hello [PIP](https://pip.pypa.io/en/stable/installing/) pakietu.
5. Aktualizacja adresu PIP toohello najnowszej wersji, uruchamiając hello `pip install -U pip` polecenia.
6. Zainstalować łącznik MySQL hello Python i jego zależności za pomocą polecenia PIP hello:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj hello serwera, musisz mieć wydłużało, takich jak **myserver4demo**.
3. Kliknij nazwę serwera hello **myserver4demo**.
4. Wybierz powitania serwera **właściwości** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-python/1_server-properties-name-login.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.
   

## <a name="run-python-code"></a>Uruchamianie kodu języka Python
- Wklej hello kod do pliku tekstowego, a następnie zapisz plik hello do folderu projektu z PY i rozszerzenia plików, na przykład C:\pythonmysql\createtable.py lub /home/username/pythonmysql/createtable.py
- Kod hello toorun, uruchom wiersz polecenia hello lub powłoki bash. Zmień katalog na folder projektu `cd pythonmysql`. Następnie wpisz polecenie python hello następuje nazwa pliku hello `python createtable.py` toorun hello aplikacji. Na powitania systemu operacyjnego Windows Jeśli python.exe nie zostanie znaleziony, możesz podać hello — toohello Pełna ścieżka pliku wykonywalnego lub Dodaj hello Python ścieżki do zmiennej środowiskowej path hello. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych
Użyj następujących hello kodu serwera toohello tooconnect, Utwórz tabelę i załadować hello danych przy użyciu **Wstaw** instrukcji SQL. 

W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane. Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello. Kod Hello korzysta z kursora hello połączenia i i [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje zapytanie SQL hello w bazie danych MySQL. 

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. 

W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane. Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello. Kod Hello korzysta z kursora na powitania połączenia, a [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje instrukcję SQL hello w bazie danych MySQL. wiersze danych Hello są odczytywane przy użyciu hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) metody. Witaj zestaw wyników jest przechowywany w kolekcji wiersza i iteratora jest tooloop używanych przez hello wierszy.

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL. 

W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane.  Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello. Kod Hello korzysta z kursora na powitania połączenia, a [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje instrukcję SQL hello w bazie danych MySQL. 

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i usuwanie danych przy użyciu **usunąć** instrukcji SQL. 

W kodzie hello hello mysql.connector biblioteki zostaną zaimportowane.  Witaj [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funkcja jest używana tooconnect tooAzure bazy danych dla programu MySQL przy użyciu hello [argumenty połączenia](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) w kolekcji config hello. Kod Hello korzysta z kursora hello połączenia i i [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metoda wykonuje zapytanie SQL hello w bazie danych MySQL. 

Zastąp hello `host`, `user`, `password`, i `database` parametry z wartościami hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./concepts-migrate-import-export.md)
