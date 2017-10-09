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
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="226a1-103">Bazy danych platformy Azure dla PostgreSQL: Użyj Przejdź tooconnect i zapytań danych przy użyciu języka</span><span class="sxs-lookup"><span data-stu-id="226a1-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="226a1-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan bazy danych platformy Azure dla PostgreSQL przy użyciu kodu hello napisanych w [Przejdź](https://golang.org/) języka (golang).</span><span class="sxs-lookup"><span data-stu-id="226a1-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="226a1-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="226a1-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="226a1-106">W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Go, ale, czy są nowe tooworking z bazą danych Azure dla PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="226a1-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="226a1-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="226a1-107">Prerequisites</span></span>
<span data-ttu-id="226a1-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="226a1-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="226a1-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="226a1-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="226a1-110">Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="226a1-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="226a1-111">Instalowanie łączników języków Go i pq</span><span class="sxs-lookup"><span data-stu-id="226a1-111">Install Go and pq connector</span></span>
<span data-ttu-id="226a1-112">Zainstaluj [Przejdź](https://golang.org/doc/install) i hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) na własnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="226a1-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="226a1-113">W zależności od platformy wykonaj kroki hello:</span><span class="sxs-lookup"><span data-stu-id="226a1-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="226a1-114">Windows</span><span class="sxs-lookup"><span data-stu-id="226a1-114">Windows</span></span>
1. <span data-ttu-id="226a1-115">[Pobierz](https://golang.org/dl/) i zainstalować Go systemu Microsoft Windows zgodnie z toohello [instrukcje dotyczące instalacji](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="226a1-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="226a1-116">Uruchom wiersz polecenia hello z hello start menu.</span><span class="sxs-lookup"><span data-stu-id="226a1-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="226a1-117">Utwórz folder dla projektu, np.</span><span class="sxs-lookup"><span data-stu-id="226a1-117">Make a folder for your project such.</span></span> <span data-ttu-id="226a1-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="226a1-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="226a1-119">Zmień katalog na folder projektu hello, takich jak `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="226a1-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="226a1-120">Ustaw zmienne środowiskowe hello do katalogu kodu źródłowego toohello toopoint GOPATH.</span><span class="sxs-lookup"><span data-stu-id="226a1-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="226a1-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="226a1-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="226a1-122">Zainstaluj hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) uruchamiając hello `go get github.com/lib/pq` polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="226a1-123">Podsumowując Zainstaluj Go, a następnie uruchom następujące polecenia w wierszu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="226a1-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="226a1-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="226a1-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="226a1-125">Uruchom program hello powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="226a1-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="226a1-126">Zainstaluj środowisko języka Go, uruchamiając polecenie `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="226a1-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="226a1-127">Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="226a1-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="226a1-128">Zmień katalog na hello folder, takich jak `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="226a1-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="226a1-129">Zestaw hello GOPATH środowiska zmiennej toopoint tooa prawidłowe źródło katalogu, takiego jak domu bieżący folder przejdź do katalogu.</span><span class="sxs-lookup"><span data-stu-id="226a1-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="226a1-130">W hello powłoki bash, uruchom `export GOPATH=~/go` tooadd hello Przejdź katalogu jako hello GOPATH dla bieżącej sesji powłoki hello.</span><span class="sxs-lookup"><span data-stu-id="226a1-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="226a1-131">Zainstaluj hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) uruchamiając hello `go get github.com/lib/pq` polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="226a1-132">Podsumowując: uruchom te polecenia programu Bash:</span><span class="sxs-lookup"><span data-stu-id="226a1-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="226a1-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="226a1-133">Apple macOS</span></span>
1. <span data-ttu-id="226a1-134">Pobierz i zainstaluj Go zgodnie z toohello [instrukcje dotyczące instalacji](https://golang.org/doc/install) platformy do dopasowania.</span><span class="sxs-lookup"><span data-stu-id="226a1-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="226a1-135">Uruchom program hello powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="226a1-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="226a1-136">Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="226a1-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="226a1-137">Zmień katalog na hello folder, takich jak `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="226a1-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="226a1-138">Zestaw hello GOPATH środowiska zmiennej toopoint tooa prawidłowe źródło katalogu, takiego jak domu bieżący folder przejdź do katalogu.</span><span class="sxs-lookup"><span data-stu-id="226a1-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="226a1-139">W hello powłoki bash, uruchom `export GOPATH=~/go` tooadd hello Przejdź katalogu jako hello GOPATH dla bieżącej sesji powłoki hello.</span><span class="sxs-lookup"><span data-stu-id="226a1-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="226a1-140">Zainstaluj hello [czysty Postgres Przejdź sterownika (pq)](https://github.com/lib/pq) uruchamiając hello `go get github.com/lib/pq` polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="226a1-141">Podsumowując: zainstaluj środowisko języka Go, następnie uruchom te polecenia programu Bash:</span><span class="sxs-lookup"><span data-stu-id="226a1-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="226a1-142">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="226a1-142">Get connection information</span></span>
<span data-ttu-id="226a1-143">Pobierz PostgreSQL hello połączenia potrzebnych tooconnect toohello bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="226a1-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="226a1-144">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="226a1-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="226a1-145">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="226a1-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="226a1-146">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="226a1-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="226a1-147">Kliknij nazwę serwera hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="226a1-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="226a1-148">Wybierz powitania serwera **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="226a1-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="226a1-149">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="226a1-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="226a1-150">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="226a1-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="226a1-151">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony i nazwę logowania administratora serwera hello widoku.</span><span class="sxs-lookup"><span data-stu-id="226a1-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="226a1-152">W razie potrzeby Zresetuj hello hasło.</span><span class="sxs-lookup"><span data-stu-id="226a1-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="226a1-153">Kompilowanie i uruchamianie kodu języka Go</span><span class="sxs-lookup"><span data-stu-id="226a1-153">Build and run Go code</span></span> 
1. <span data-ttu-id="226a1-154">toowrite Golang kodu, można użyć edytora zwykłego tekstu, takiego jak Notatnik w systemie Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) lub [Nano](https://www.nano-editor.org/) Ubuntu lub TextEdit w macOS.</span><span class="sxs-lookup"><span data-stu-id="226a1-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="226a1-155">Jeśli wolisz bardziej zaawansowane środowisko IDE, wypróbuj rozwiązanie [Gogland](https://www.jetbrains.com/go/) firmy Jetbrains, edytor [Visual Studio Code](https://code.visualstudio.com/) firmy Microsoft lub [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="226a1-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="226a1-156">Wklej kod Golang hello z sekcjami hello do plików tekstowych i zapisać w folderze projektu z rozszerzeniem pliku \*.go, takich jak ścieżki systemu Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` lub ścieżka systemu Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="226a1-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="226a1-157">Zlokalizuj hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` stałe w kodzie hello i Zastąp hello przykładowe wartości z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="226a1-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="226a1-158">Uruchom wiersz polecenia hello lub powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="226a1-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="226a1-159">Przejdź do folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="226a1-159">Change directory into your project folder.</span></span> <span data-ttu-id="226a1-160">Na przykład w systemie Windows uruchom polecenie `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="226a1-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="226a1-161">W systemie Linux: `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="226a1-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="226a1-162">Niektóre z wymienionych środowiska IDE hello oferują możliwości debugowania i środowiska uruchomieniowego bez konieczności poleceń powłoki.</span><span class="sxs-lookup"><span data-stu-id="226a1-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="226a1-163">Uruchom kod hello, wpisując polecenie hello `go run createtable.go` toocompile hello aplikacji i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="226a1-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="226a1-164">Alternatywnie toobuild hello kodu do natywnej aplikacji, `go build createtable.go`, uruchom `createtable.exe` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="226a1-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="226a1-165">Łączenie i tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="226a1-165">Connect and create a table</span></span>
<span data-ttu-id="226a1-166">Użyj hello następujący kod tooconnect i utworzyć przy użyciu tabeli **CREATE TABLE** instrukcji SQL, a następnie **INSERT INTO** SQL instrukcje tooadd wiersze w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="226a1-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="226a1-167">Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="226a1-168">Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="226a1-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="226a1-169">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="226a1-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="226a1-170">Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun kilka razy kilka poleceń SQL.</span><span class="sxs-lookup"><span data-stu-id="226a1-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="226a1-171">Każdy czas toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="226a1-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="226a1-172">Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="226a1-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="226a1-173">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="226a1-173">Read data</span></span>
<span data-ttu-id="226a1-174">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="226a1-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="226a1-175">Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="226a1-176">Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="226a1-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="226a1-177">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="226a1-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="226a1-178">Zapytanie select Hello jest uruchamiany przez wywołanie metody [bazy danych. Query()](https://golang.org/pkg/database/sql/#DB.Query), i hello zwrócone wiersze są przechowywane w zmiennej typu [wierszy](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="226a1-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="226a1-179">Kod Hello odczytuje wartości danych kolumn hello hello bieżącego wiersza przy użyciu metody [wierszy. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) i pętli za pośrednictwem hello wiersze, używając iteratora hello [wierszy. Next()](https://golang.org/pkg/database/sql/#Rows.Next) dopóki nie istnieją żadne więcej wierszy.</span><span class="sxs-lookup"><span data-stu-id="226a1-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="226a1-180">Każdy wiersz wartości w kolumnie są konsoli drukowanej toohello wychodzących. Każdy czas toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="226a1-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="226a1-181">Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="226a1-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="226a1-182">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="226a1-182">Update data</span></span>
<span data-ttu-id="226a1-183">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="226a1-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="226a1-184">Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="226a1-185">Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="226a1-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="226a1-186">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="226a1-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="226a1-187">Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun hello instrukcji SQL, która aktualizuje hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="226a1-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="226a1-188">Toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli błąd wystąpi.</span><span class="sxs-lookup"><span data-stu-id="226a1-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="226a1-189">Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="226a1-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="delete-data"></a><span data-ttu-id="226a1-190">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="226a1-190">Delete data</span></span>
<span data-ttu-id="226a1-191">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="226a1-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="226a1-192">Hello kod importuje pakiety trzy: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [pakietu pq](http://godoc.org/github.com/lib/pq) jako toocommunicate sterowników, z serwerem Postgres hello i hello [pakietu formatowaniu](https://golang.org/pkg/fmt/) dla drukowane dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="226a1-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="226a1-193">Witaj kod wywołuje metodę [sql. Metody Open()](http://godoc.org/github.com/lib/pq#Open) tooAzure tooconnect bazy danych dla PostgreSQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="226a1-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="226a1-194">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="226a1-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="226a1-195">Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun hello instrukcji SQL, która aktualizuje hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="226a1-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="226a1-196">Toocheck metody checkError() niestandardowych, jeśli wystąpił błąd i awaryjne tooexit, jeśli błąd wystąpi.</span><span class="sxs-lookup"><span data-stu-id="226a1-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="226a1-197">Zastąp hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` parametrów z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="226a1-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="226a1-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="226a1-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="226a1-199">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="226a1-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
