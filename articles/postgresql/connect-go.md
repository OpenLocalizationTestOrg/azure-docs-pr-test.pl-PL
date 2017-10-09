---
title: "tooAzure aaaConnect bazy danych przy użyciu języka Przejdź PostgreSQL | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera Przejdź programowania języka przykładowy można użyć tooconnect i wyszukiwać dane z bazy danych Azure PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla PostgreSQL: Użyj Przejdź tooconnect i zapytań danych przy użyciu języka
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan bazy danych platformy Azure dla PostgreSQL przy użyciu kodu hello napisanych w [Przejdź](https://golang.org/) języka (golang). Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Go, ale, czy są nowe tooworking z bazą danych Azure dla PostgreSQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie bazy danych — portal](quickstart-create-server-database-portal.md)
- [Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Instalowanie łączników języków Go i pq
Zainstaluj [Przejdź](https://golang.org/doc/install) i hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) na własnym komputerze. W zależności od platformy wykonaj kroki hello:

### <a name="windows"></a>Windows
1. [Pobierz](https://golang.org/dl/) i zainstalować Go systemu Microsoft Windows zgodnie z toohello [instrukcje dotyczące instalacji](https://golang.org/doc/install).
2. Uruchom wiersz polecenia hello z hello start menu.
3. Utwórz folder dla projektu, np. `mkdir  %USERPROFILE%\go\src\postgresqlgo`.
4. Zmień katalog na folder projektu hello, takich jak `cd %USERPROFILE%\go\src\postgresqlgo`.
5. Ustaw zmienne środowiskowe hello do katalogu kodu źródłowego toohello toopoint GOPATH. `set GOPATH=%USERPROFILE%\go`.
6. Zainstaluj hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) uruchamiając hello `go get github.com/lib/pq` polecenia.

   Podsumowując Zainstaluj Go, a następnie uruchom następujące polecenia w wierszu polecenia hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Uruchom program hello powłoki Bash. 
2. Zainstaluj środowisko języka Go, uruchamiając polecenie `sudo apt-get install golang-go`.
3. Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/postgresqlgo/`.
4. Zmień katalog na hello folder, takich jak `cd ~/go/src/postgresqlgo/`.
5. Zestaw hello GOPATH środowiska zmiennej toopoint tooa prawidłowe źródło katalogu, takiego jak domu bieżący folder przejdź do katalogu. W hello powłoki bash, uruchom `export GOPATH=~/go` tooadd hello Przejdź katalogu jako hello GOPATH dla bieżącej sesji powłoki hello.
6. Zainstaluj hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) uruchamiając hello `go get github.com/lib/pq` polecenia.

   Podsumowując: uruchom te polecenia programu Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>Apple macOS
1. Pobierz i zainstaluj Go zgodnie z toohello [instrukcje dotyczące instalacji](https://golang.org/doc/install) platformy do dopasowania. 
2. Uruchom program hello powłoki Bash. 
3. Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/postgresqlgo/`.
4. Zmień katalog na hello folder, takich jak `cd ~/go/src/postgresqlgo/`.
5. Zestaw hello GOPATH środowiska zmiennej toopoint tooa prawidłowe źródło katalogu, takiego jak domu bieżący folder przejdź do katalogu. W hello powłoki bash, uruchom `export GOPATH=~/go` tooadd hello Przejdź katalogu jako hello GOPATH dla bieżącej sesji powłoki hello.
6. Zainstaluj hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) uruchamiając hello `go get github.com/lib/pq` polecenia.

   Podsumowując: zainstaluj środowisko języka Go, następnie uruchom te polecenia programu Bash:
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **mypgserver 20170401**.
3. Kliknij nazwę serwera hello **mypgserver 20170401**.
4. Wybierz powitania serwera **omówienie** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-go/1-connection-string.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony i nazwę logowania administratora serwera hello widoku. W razie potrzeby Zresetuj hello hasło.

## <a name="build-and-run-go-code"></a>Kompilowanie i uruchamianie kodu języka Go 
1. toowrite Golang kodu, można użyć edytora zwykłego tekstu, takiego jak Notatnik w systemie Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) lub [Nano](https://www.nano-editor.org/) Ubuntu lub TextEdit w macOS. Jeśli wolisz bardziej zaawansowane środowisko IDE, wypróbuj rozwiązanie [Gogland](https://www.jetbrains.com/go/) firmy Jetbrains, edytor [Visual Studio Code](https://code.visualstudio.com/) firmy Microsoft lub [Atom](https://atom.io/).
2. Wklej kod Golang hello z sekcjami hello do plików tekstowych i zapisać w folderze projektu z rozszerzeniem pliku \*.go, takich jak ścieżki systemu Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` lub ścieżka systemu Linux `~/go/src/postgresqlgo/createtable.go`.
3. Zlokalizuj hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` stałe w kodzie hello i Zastąp hello przykładowe wartości z własne wartości.  
4. Uruchom wiersz polecenia hello lub powłoki bash. Przejdź do folderu projektu. Na przykład w systemie Windows uruchom polecenie `cd %USERPROFILE%\go\src\postgresqlgo\`. W systemie Linux: `cd ~/go/src/postgresqlgo/`. Niektóre z wymienionych środowiska IDE hello oferują możliwości debugowania i środowiska uruchomieniowego bez konieczności poleceń powłoki.
5. Uruchom kod hello, wpisując polecenie hello `go run createtable.go` toocompile hello aplikacji i uruchom go. 
6. Alternatywnie toobuild hello kodu do natywnej aplikacji, `go build createtable.go`, uruchom `createtable.exe` toorun hello aplikacji.

## <a name="connect-and-create-a-table"></a>Łączenie i tworzenie tabeli
Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.

Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.

Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych. Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun kilka razy kilka poleceń SQL. Każdy czas toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli wystąpi błąd.

Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a>Odczyt danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. 

Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.

Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych. Zapytanie select Hello jest uruchamiany przez wywołanie metody [bazy danych. Query()](https://golang.org/pkg/database/sql/#DB.Query), i hello zwrócone wiersze są przechowywane w zmiennej typu [wierszy](https://golang.org/pkg/database/sql/#Rows). Kod Hello odczytuje wartości danych kolumn hello hello bieżącego wiersza przy użyciu metody [wierszy. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) i pętli za pośrednictwem hello wiersze, używając iteratora hello [wierszy. Next()](https://golang.org/pkg/database/sql/#Rows.Next) dopóki nie istnieją żadne więcej wierszy. Każdy wiersz wartości w kolumnie są konsoli drukowanej toohello wychodzących. Każdy czas toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli wystąpi błąd.

Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.

Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.

Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych. Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun hello instrukcji SQL, która aktualizuje hello tabeli. Toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli błąd wystąpi.

Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. 

Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.

Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych. Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun hello instrukcji SQL, która aktualizuje hello tabeli. Toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli błąd wystąpi.

Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./howto-migrate-using-export-and-import.md)
