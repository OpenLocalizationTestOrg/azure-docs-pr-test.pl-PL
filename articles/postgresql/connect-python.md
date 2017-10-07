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
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla PostgreSQL: Użyj Python tooconnect i zapytań danych
Ta opcja szybkiego startu przedstawia sposób toouse [Python](https://python.org) tooan tooconnect PostgreSQL bazy danych Azure. Przedstawiono również sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello macOS, Ubuntu Linux i platform Windows. Witaj opisanych w tym artykule założono, że znasz tworzenie przy użyciu języka Python i są nowe tooworking z bazą danych Azure dla PostgreSQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie bazy danych — portal](quickstart-create-server-database-portal.md)
- [Tworzenie bazy danych — interfejs wiersza polecenia](quickstart-create-server-database-azure-cli.md)

Wymagane są również:
- Zainstalowany język [python](https://www.python.org/downloads/)
- Zainstalowany pakiet [pip](https://pip.pypa.io/en/stable/installing/) (pakiet pip jest już zainstalowany, jeśli używasz plików binarnych języka Python 2 w wersji 2.7.9 lub nowszej albo Python 3 w wersji 3.4 lub nowszej pobranych z witryny [python.org](https://python.org)).

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>Zainstaluj biblioteki połączeń hello języka Python dla PostgreSQL
Zainstaluj hello [psycopg2](http://initd.org/psycopg/docs/install.html) pakiet, który umożliwia tooconnect i zapytań hello bazy danych. jest psycopg2 [dostępne na PyPI](https://pypi.python.org/pypi/psycopg2/) w formie hello [koło](http://pythonwheels.com/) pakietów hello najczęściej platform (z systemem Linux, OS x, Windows). Użyj pip zainstalować tooget hello binarna wersja modułu hello wraz z zależnościami hello wszystkie.

1. Na komputerze uruchom interfejs wiersza polecenia:
    - W systemie Linux Uruchom hello powłoki Bash.
    - Po macOS Uruchom hello terminalu.
    - W systemie Windows uruchom program hello wiersz polecenia z hello Start Menu.
2. Upewnij się, że używasz najnowszej wersji narzędzia pip hello za pomocą polecenia takie jak:
    ```cmd
    pip install -U pip
    ```

3. Uruchom następujące polecenie tooinstall hello psycopg2 pakietów hello:
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj **mypgserver 20170401** (serwer hello właśnie utworzony).
3. Kliknij nazwę serwera hello **mypgserver 20170401**.
4. Wybierz powitania serwera **omówienie** strony, a następnie zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-python/1-connection-string.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="how-toorun-python-code"></a>Jak toorun kodu języka Python
Ten temat zawiera łącznie cztery przykłady kodu, z których każdy wykonuje konkretną funkcję. Witaj poniższe instrukcje wskazują sposób Wstaw blok kodu toocreate pliku tekstowego, a następnie zapisz plik hello, tak, aby uruchomić ją później. Należy się toocreate czterech oddzielnych plików, po jednej dla każdego bloku kodu.

- W swoim ulubionym edytorze tekstów utwórz nowy plik.
- Skopiuj i Wklej jedną z próbek kodu hello w hello następujące sekcje w pliku tekstowym hello. Zastąp hello **hosta**, **dbname**, **użytkownika**, i **hasło** parametry z wartościami hello określone podczas tworzenia hello serwer i bazę danych.
- Zapisz hello plik z rozszerzeniem .py hello (na przykład postgres.py) w folderze projektu. Jeśli korzystasz z systemu operacyjnego Windows hello, należy się tooselect kodowania UTF-8 podczas zapisywania pliku hello. 
- Uruchom powłokę wiersza polecenia lub Bash hello, a następnie zmień folder tooyour hello katalogu projektu, na przykład `cd postgres`.
-  Kod hello toorun, hello typ polecenia języka Python, następuje hello nazwę pliku, na przykład `Python postgres.py`.

> [!NOTE]
> Począwszy od języka Python w wersji 3, może zostać wyświetlony błąd hello `SyntaxError: Missing parentheses in call too'print'` podczas uruchamiania powitania po bloków kodu. Jeśli tak się stanie, Zastąp każde polecenie toohello wywołania `print "string"` z wywołania funkcji przy użyciu nawias, takich jak `print("string")`.

## <a name="connect-create-table-and-insert-data"></a>Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych
Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) działać z **Wstaw** instrukcji SQL. Witaj [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funkcji jest używane tooexecute hello zapytanie SQL bazy danych PostgreSQL. Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.

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

Po hello kodu zostanie wykonane pomyślnie, dane wyjściowe hello wygląda następująco:

![Dane wyjściowe wiersza polecenia](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>Odczyt danych
Użyj hello poniższy kod tooread hello danych za pomocą [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) działać z **wybierz** instrukcji SQL. Ta funkcja akceptuje zapytania i zwraca zestawu wyników, które można powtórzyć za pośrednictwem z użyciem hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall). Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello poniższy kod tooupdate hello spisu wiersza, który został wcześniej wstawiony przy użyciu [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) działać z **aktualizacji** instrukcji SQL. Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="delete-data"></a>Usuwanie danych
Użyj hello poniższy kod toodelete elementu spisu, który wcześniej wstawiony przy użyciu [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) działać z **usunąć** instrukcji SQL. Zamień hello hosta, dbname użytkownika i hasło Parametry wartości hello określone podczas tworzenia powitania serwera i bazy danych.

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

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./howto-migrate-using-export-and-import.md)
