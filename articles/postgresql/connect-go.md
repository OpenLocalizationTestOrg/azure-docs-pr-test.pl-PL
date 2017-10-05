---
title: "Nawiązywanie połączeń z usługą Azure Database for PostgreSQL za pomocą języka Go | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera przykładowy języka programowania Go, którego można używać do nawiązywania połączeń z danymi usługi Azure Database for PostgreSQL i wykonywania zapytań względem nich."
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
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="f76ba-103">Usługa Azure Database for PostgreSQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą języka Go</span><span class="sxs-lookup"><span data-stu-id="f76ba-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="f76ba-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for PostgreSQL przy użyciu kodu napisanego w języku [Go](https://golang.org/) (golang).</span><span class="sxs-lookup"><span data-stu-id="f76ba-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="f76ba-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f76ba-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="f76ba-106">W tym artykule założono, że wiesz już, jak programować za pomocą języka Go, i dopiero zaczynasz pracę z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f76ba-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f76ba-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f76ba-107">Prerequisites</span></span>
<span data-ttu-id="f76ba-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="f76ba-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="f76ba-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="f76ba-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="f76ba-110">Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f76ba-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="f76ba-111">Instalowanie łączników języków Go i pq</span><span class="sxs-lookup"><span data-stu-id="f76ba-111">Install Go and pq connector</span></span>
<span data-ttu-id="f76ba-112">Zainstaluj język [Go](https://golang.org/doc/install) i [sterownik Pure Go Postgres (pq)](https://github.com/lib/pq) na własnej maszynie.</span><span class="sxs-lookup"><span data-stu-id="f76ba-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="f76ba-113">W zależności od używanej platformy wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f76ba-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="f76ba-114">Windows</span><span class="sxs-lookup"><span data-stu-id="f76ba-114">Windows</span></span>
1. <span data-ttu-id="f76ba-115">[Pobierz](https://golang.org/dl/) i zainstaluj środowisko języka Go dla systemu Microsoft Windows zgodnie z [instrukcjami dotyczącymi instalacji](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="f76ba-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="f76ba-116">Uruchom wiersz polecenia z menu Start.</span><span class="sxs-lookup"><span data-stu-id="f76ba-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="f76ba-117">Utwórz folder dla projektu, np.</span><span class="sxs-lookup"><span data-stu-id="f76ba-117">Make a folder for your project such.</span></span> <span data-ttu-id="f76ba-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="f76ba-119">Przejdź do folderu projektu, np. `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="f76ba-120">Ustaw zmienną środowiskową GOPATH, aby wskazywała katalog kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="f76ba-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="f76ba-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="f76ba-122">Zainstaluj [sterownik Pure Go Postgres (pq)](https://github.com/lib/pq), uruchamiając polecenie `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="f76ba-123">Podsumowując: zainstaluj środowisko języka Go, a następnie uruchom następujące polecenia w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="f76ba-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="f76ba-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f76ba-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="f76ba-125">Uruchom powłokę Bash.</span><span class="sxs-lookup"><span data-stu-id="f76ba-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="f76ba-126">Zainstaluj środowisko języka Go, uruchamiając polecenie `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="f76ba-127">Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="f76ba-128">Przejdź do tego folderu, np. `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="f76ba-129">Ustaw zmienną środowiskową GOPATH tak, aby wskazywała prawidłowy katalog źródłowy, np. folder go w bieżącym katalogu macierzystym.</span><span class="sxs-lookup"><span data-stu-id="f76ba-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="f76ba-130">W powłoce Bash uruchom polecenie `export GOPATH=~/go`, aby dodać katalog go jako zmienną GOPATH dla bieżącej sesji powłoki.</span><span class="sxs-lookup"><span data-stu-id="f76ba-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="f76ba-131">Zainstaluj [sterownik Pure Go Postgres (pq)](https://github.com/lib/pq), uruchamiając polecenie `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="f76ba-132">Podsumowując: uruchom te polecenia programu Bash:</span><span class="sxs-lookup"><span data-stu-id="f76ba-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="f76ba-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="f76ba-133">Apple macOS</span></span>
1. <span data-ttu-id="f76ba-134">Pobierz i zainstaluj język Go zgodnie z [instrukcjami dotyczącymi instalacji](https://golang.org/doc/install) odpowiedniej platformy.</span><span class="sxs-lookup"><span data-stu-id="f76ba-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="f76ba-135">Uruchom powłokę Bash.</span><span class="sxs-lookup"><span data-stu-id="f76ba-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="f76ba-136">Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="f76ba-137">Przejdź do tego folderu, np. `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="f76ba-138">Ustaw zmienną środowiskową GOPATH tak, aby wskazywała prawidłowy katalog źródłowy, np. folder go w bieżącym katalogu macierzystym.</span><span class="sxs-lookup"><span data-stu-id="f76ba-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="f76ba-139">W powłoce Bash uruchom polecenie `export GOPATH=~/go`, aby dodać katalog go jako zmienną GOPATH dla bieżącej sesji powłoki.</span><span class="sxs-lookup"><span data-stu-id="f76ba-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="f76ba-140">Zainstaluj [sterownik Pure Go Postgres (pq)](https://github.com/lib/pq), uruchamiając polecenie `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="f76ba-141">Podsumowując: zainstaluj środowisko języka Go, następnie uruchom te polecenia programu Bash:</span><span class="sxs-lookup"><span data-stu-id="f76ba-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="f76ba-142">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="f76ba-142">Get connection information</span></span>
<span data-ttu-id="f76ba-143">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f76ba-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="f76ba-144">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="f76ba-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="f76ba-145">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f76ba-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f76ba-146">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="f76ba-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="f76ba-147">Kliknij nazwę serwera **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="f76ba-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="f76ba-148">Wybierz stronę serwera **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="f76ba-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="f76ba-149">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="f76ba-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="f76ba-150">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="f76ba-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="f76ba-151">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd** i wyświetl nazwę logowania administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="f76ba-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="f76ba-152">W razie potrzeby zresetuj hasło.</span><span class="sxs-lookup"><span data-stu-id="f76ba-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="f76ba-153">Kompilowanie i uruchamianie kodu języka Go</span><span class="sxs-lookup"><span data-stu-id="f76ba-153">Build and run Go code</span></span> 
1. <span data-ttu-id="f76ba-154">Do pisania kodu w języku Golang można użyć prostego edytora tekstów, takiego jak Notatnik w systemie Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) lub [Nano](https://www.nano-editor.org/) w systemie Ubuntu lub TextEdit w systemie macOS.</span><span class="sxs-lookup"><span data-stu-id="f76ba-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="f76ba-155">Jeśli wolisz bardziej zaawansowane środowisko IDE, wypróbuj rozwiązanie [Gogland](https://www.jetbrains.com/go/) firmy Jetbrains, edytor [Visual Studio Code](https://code.visualstudio.com/) firmy Microsoft lub [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="f76ba-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="f76ba-156">Wklej kod języka Golang z poniższych sekcji do plików tekstowych i zapisz pliki w folderze projektu z rozszerzeniem pliku \*.go. Na przykład ścieżka w systemie Windows: `%USERPROFILE%\go\src\postgresqlgo\createtable.go`, ścieżka w systemie Linux: `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="f76ba-157">Zlokalizuj zmienne `HOST`, `DATABASE`, `USER` i `PASSWORD` w kodzie i zastąp przykładowe wartości wybranymi samodzielnie wartościami.</span><span class="sxs-lookup"><span data-stu-id="f76ba-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="f76ba-158">Uruchom wiersz polecenia lub powłokę bash.</span><span class="sxs-lookup"><span data-stu-id="f76ba-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="f76ba-159">Przejdź do folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="f76ba-159">Change directory into your project folder.</span></span> <span data-ttu-id="f76ba-160">Na przykład w systemie Windows uruchom polecenie `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="f76ba-161">W systemie Linux: `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f76ba-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="f76ba-162">Niektóre z wymienionych środowisk IDE oferują możliwości debugowania i uruchamiania bez konieczności używania poleceń powłoki.</span><span class="sxs-lookup"><span data-stu-id="f76ba-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="f76ba-163">Uruchom kod, wpisując polecenie `go run createtable.go`, aby skompilować aplikację i uruchomić ją.</span><span class="sxs-lookup"><span data-stu-id="f76ba-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="f76ba-164">Alternatywnie, aby skompilować kod w aplikację natywną, uruchom polecenie `go build createtable.go`, a następnie uruchom plik `createtable.exe` w celu uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f76ba-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="f76ba-165">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="f76ba-165">Connect and create a table</span></span>
<span data-ttu-id="f76ba-166">Użyj poniższego kodu w celu nawiązania połączenia i utworzenia tabeli za pomocą instrukcji **CREATE TABLE** języka SQL, a następnie instrukcji **INSERT INTO** języka SQL, aby dodać wiersze do tabeli.</span><span class="sxs-lookup"><span data-stu-id="f76ba-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="f76ba-167">Kod importuje trzy pakiety: [pakiet sql](https://golang.org/pkg/database/sql/), [pakiet pq](http://godoc.org/github.com/lib/pq) jako sterownik do komunikacji z serwerem Postgres i [pakiet fmt](https://golang.org/pkg/fmt/) dla drukowanych danych wejściowych i wyjściowych w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f76ba-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f76ba-168">Kod wywołuje metodę [sql.Open()](http://godoc.org/github.com/lib/pq#Open), aby nawiązać połączenie z usługą bazą danych Azure Database for PostgreSQL, i sprawdza połączenie przy użyciu metody [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f76ba-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f76ba-169">Używane jest [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB), które utrzymuje pulę połączeń dla serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f76ba-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f76ba-170">Kod wywołuje metodę [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) kilka razy, aby uruchomić kilka poleceń SQL.</span><span class="sxs-lookup"><span data-stu-id="f76ba-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="f76ba-171">Za każdym razem jest wywoływana niestandardowa metoda checkError() w celu sprawdzenia, czy wystąpił błąd, i awaryjnego zakończenia pracy w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="f76ba-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f76ba-172">Zastąp parametry `HOST`, `DATABASE`, `USER` i `PASSWORD` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="f76ba-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="read-data"></a><span data-ttu-id="f76ba-173">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="f76ba-173">Read data</span></span>
<span data-ttu-id="f76ba-174">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="f76ba-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="f76ba-175">Kod importuje trzy pakiety: [pakiet sql](https://golang.org/pkg/database/sql/), [pakiet pq](http://godoc.org/github.com/lib/pq) jako sterownik do komunikacji z serwerem Postgres i [pakiet fmt](https://golang.org/pkg/fmt/) dla drukowanych danych wejściowych i wyjściowych w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f76ba-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f76ba-176">Kod wywołuje metodę [sql.Open()](http://godoc.org/github.com/lib/pq#Open), aby nawiązać połączenie z usługą bazą danych Azure Database for PostgreSQL, i sprawdza połączenie przy użyciu metody [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f76ba-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f76ba-177">Używane jest [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB), które utrzymuje pulę połączeń dla serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f76ba-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f76ba-178">Zapytanie dotyczące instrukcji select jest uruchamiane przez wywołanie metody [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), a wiersze wynikowe są przechowywane w zmiennej typu [rows](https://golang.org/pkg/database/sql/#Rows) (wiersze).</span><span class="sxs-lookup"><span data-stu-id="f76ba-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="f76ba-179">Kod odczytuje wartości danych kolumny danych w bieżącym wierszu przy użyciu metody [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) i wykonuje operacje dla wierszy w pętli, używając iteratora [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) do momentu, gdy nie ma już kolejnych wierszy.</span><span class="sxs-lookup"><span data-stu-id="f76ba-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="f76ba-180">Wartości kolumn w każdym wierszu są drukowane do konsoli. Za każdym razem jest wywoływana niestandardowa metoda checkError() w celu sprawdzenia, czy wystąpił błąd, i awaryjnego zakończenia pracy w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="f76ba-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f76ba-181">Zastąp parametry `HOST`, `DATABASE`, `USER` i `PASSWORD` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="f76ba-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="update-data"></a><span data-ttu-id="f76ba-182">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="f76ba-182">Update data</span></span>
<span data-ttu-id="f76ba-183">Użyj poniższego kodu, aby nawiązać połączenie i zaktualizować dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="f76ba-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="f76ba-184">Kod importuje trzy pakiety: [pakiet sql](https://golang.org/pkg/database/sql/), [pakiet pq](http://godoc.org/github.com/lib/pq) jako sterownik do komunikacji z serwerem Postgres i [pakiet fmt](https://golang.org/pkg/fmt/) dla drukowanych danych wejściowych i wyjściowych w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f76ba-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f76ba-185">Kod wywołuje metodę [sql.Open()](http://godoc.org/github.com/lib/pq#Open), aby nawiązać połączenie z usługą bazą danych Azure Database for PostgreSQL, i sprawdza połączenie przy użyciu metody [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f76ba-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f76ba-186">Używane jest [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB), które utrzymuje pulę połączeń dla serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f76ba-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f76ba-187">Kod wywołuje metodę [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) w celu uruchomienia instrukcji SQL służącej do aktualizowania tabeli.</span><span class="sxs-lookup"><span data-stu-id="f76ba-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="f76ba-188">Niestandardowa metoda checkError() służy do sprawdzania, czy wystąpił błąd, i awaryjnego kończenia pracy w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="f76ba-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f76ba-189">Zastąp parametry `HOST`, `DATABASE`, `USER` i `PASSWORD` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="f76ba-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="f76ba-190">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="f76ba-190">Delete data</span></span>
<span data-ttu-id="f76ba-191">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="f76ba-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="f76ba-192">Kod importuje trzy pakiety: [pakiet sql](https://golang.org/pkg/database/sql/), [pakiet pq](http://godoc.org/github.com/lib/pq) jako sterownik do komunikacji z serwerem Postgres i [pakiet fmt](https://golang.org/pkg/fmt/) dla drukowanych danych wejściowych i wyjściowych w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f76ba-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f76ba-193">Kod wywołuje metodę [sql.Open()](http://godoc.org/github.com/lib/pq#Open), aby nawiązać połączenie z usługą bazą danych Azure Database for PostgreSQL, i sprawdza połączenie przy użyciu metody [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f76ba-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f76ba-194">Używane jest [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB), które utrzymuje pulę połączeń dla serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f76ba-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f76ba-195">Kod wywołuje metodę [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) w celu uruchomienia instrukcji SQL służącej do aktualizowania tabeli.</span><span class="sxs-lookup"><span data-stu-id="f76ba-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="f76ba-196">Niestandardowa metoda checkError() służy do sprawdzania, czy wystąpił błąd, i awaryjnego kończenia pracy w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="f76ba-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f76ba-197">Zastąp parametry `HOST`, `DATABASE`, `USER` i `PASSWORD` własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="f76ba-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="f76ba-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f76ba-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f76ba-199">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="f76ba-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
