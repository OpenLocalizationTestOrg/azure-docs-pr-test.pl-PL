---
title: "Połącz tooAzure bazy danych dla programu MySQL przy użyciu przejdź | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera kilka przykładów kodu Przejdź można użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="c793f-103">Bazy danych platformy Azure dla programu MySQL: Użyj Przejdź tooconnect i zapytań danych przy użyciu języka</span><span class="sxs-lookup"><span data-stu-id="c793f-103">Azure Database for MySQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="c793f-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan bazy danych platformy Azure dla MySQL przy użyciu kodu hello napisanych w [Przejdź](https://golang.org/) języka z systemu Windows, Ubuntu Linux i Apple macOS platform.</span><span class="sxs-lookup"><span data-stu-id="c793f-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using code written in hello [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="c793f-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="c793f-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="c793f-106">W tym artykule przyjęto założenie, że znasz Programowanie przy użyciu Go, ale, czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="c793f-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c793f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c793f-107">Prerequisites</span></span>
<span data-ttu-id="c793f-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="c793f-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c793f-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c793f-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="c793f-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c793f-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="c793f-111">Instalowanie środowiska języka Go i łącznika bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="c793f-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="c793f-112">Zainstaluj [Przejdź](https://golang.org/doc/install) i hello [Przejdź sterownik sql dla programu MySQL](https://github.com/go-sql-driver/mysql#installation) na własnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c793f-112">Install [Go](https://golang.org/doc/install) and hello [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="c793f-113">W zależności od platformy wykonaj kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c793f-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="c793f-114">Windows</span><span class="sxs-lookup"><span data-stu-id="c793f-114">Windows</span></span>
1. <span data-ttu-id="c793f-115">[Pobierz](https://golang.org/dl/) i zainstalować Go systemu Microsoft Windows zgodnie z toohello [instrukcje dotyczące instalacji](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="c793f-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="c793f-116">Uruchom wiersz polecenia hello z hello start menu.</span><span class="sxs-lookup"><span data-stu-id="c793f-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="c793f-117">Utwórz folder dla projektu, np.</span><span class="sxs-lookup"><span data-stu-id="c793f-117">Make a folder for your project such.</span></span> <span data-ttu-id="c793f-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="c793f-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="c793f-119">Zmień katalog na folder projektu hello, takich jak `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="c793f-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="c793f-120">Ustaw zmienne środowiskowe hello do katalogu kodu źródłowego toohello toopoint GOPATH.</span><span class="sxs-lookup"><span data-stu-id="c793f-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="c793f-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="c793f-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="c793f-122">Zainstaluj hello [Przejdź sterownik sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) uruchamiając hello `go get github.com/go-sql-driver/mysql` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-122">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="c793f-123">Podsumowując Zainstaluj Go, a następnie uruchom następujące polecenia w wierszu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="c793f-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="c793f-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="c793f-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="c793f-125">Uruchom program hello powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="c793f-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="c793f-126">Zainstaluj środowisko języka Go, uruchamiając polecenie `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="c793f-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="c793f-127">Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="c793f-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="c793f-128">Zmień katalog na hello folder, takich jak `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="c793f-128">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="c793f-129">Zestaw hello GOPATH środowiska zmiennej toopoint tooa prawidłowe źródło katalogu, takiego jak domu bieżący folder przejdź do katalogu.</span><span class="sxs-lookup"><span data-stu-id="c793f-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="c793f-130">W hello powłoki bash, uruchom `export GOPATH=~/go` tooadd hello Przejdź katalogu jako hello GOPATH dla bieżącej sesji powłoki hello.</span><span class="sxs-lookup"><span data-stu-id="c793f-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="c793f-131">Zainstaluj hello [Przejdź sterownik sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) uruchamiając hello `go get github.com/go-sql-driver/mysql` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-131">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="c793f-132">Podsumowując: uruchom te polecenia programu Bash:</span><span class="sxs-lookup"><span data-stu-id="c793f-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="c793f-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="c793f-133">Apple macOS</span></span>
1. <span data-ttu-id="c793f-134">Pobierz i zainstaluj Go zgodnie z toohello [instrukcje dotyczące instalacji](https://golang.org/doc/install) platformy do dopasowania.</span><span class="sxs-lookup"><span data-stu-id="c793f-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="c793f-135">Uruchom program hello powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="c793f-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="c793f-136">Utwórz folder dla projektu w katalogu macierzystym, np. `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="c793f-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="c793f-137">Zmień katalog na hello folder, takich jak `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="c793f-137">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="c793f-138">Zestaw hello GOPATH środowiska zmiennej toopoint tooa prawidłowe źródło katalogu, takiego jak domu bieżący folder przejdź do katalogu.</span><span class="sxs-lookup"><span data-stu-id="c793f-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="c793f-139">W hello powłoki bash, uruchom `export GOPATH=~/go` tooadd hello Przejdź katalogu jako hello GOPATH dla bieżącej sesji powłoki hello.</span><span class="sxs-lookup"><span data-stu-id="c793f-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="c793f-140">Zainstaluj hello [Przejdź sterownik sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) uruchamiając hello `go get github.com/go-sql-driver/mysql` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-140">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="c793f-141">Podsumowując: zainstaluj środowisko języka Go, następnie uruchom te polecenia programu Bash:</span><span class="sxs-lookup"><span data-stu-id="c793f-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="c793f-142">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="c793f-142">Get connection information</span></span>
<span data-ttu-id="c793f-143">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="c793f-143">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="c793f-144">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="c793f-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c793f-145">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c793f-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c793f-146">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj hello serwera, musisz mieć wydłużało, takich jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="c793f-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="c793f-147">Kliknij nazwę serwera hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="c793f-147">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="c793f-148">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="c793f-148">Select hello server's **Properties** page.</span></span> <span data-ttu-id="c793f-149">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="c793f-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c793f-150">![Azure Database for MySQL — dane logowania administratora serwera](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="c793f-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="c793f-151">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="c793f-151">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="c793f-152">Kompilowanie i uruchamianie kodu języka Go</span><span class="sxs-lookup"><span data-stu-id="c793f-152">Build and run Go code</span></span> 
1. <span data-ttu-id="c793f-153">toowrite Golang kodu, można użyć edytora zwykłego tekstu, takiego jak Notatnik w systemie Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) lub [Nano](https://www.nano-editor.org/) Ubuntu lub TextEdit w macOS.</span><span class="sxs-lookup"><span data-stu-id="c793f-153">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="c793f-154">Jeśli wolisz bardziej zaawansowane środowisko IDE, wypróbuj rozwiązanie [Gogland](https://www.jetbrains.com/go/) firmy Jetbrains, edytor [Visual Studio Code](https://code.visualstudio.com/) firmy Microsoft lub [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="c793f-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="c793f-155">Wklej kod Go z sekcjami hello hello do plików tekstowych i zapisać w folderze projektu z rozszerzeniem pliku \*.go, takich jak ścieżki systemu Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` lub ścieżka systemu Linux `~/go/src/mysqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="c793f-155">Paste hello Go code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="c793f-156">Zlokalizuj hello `HOST`, `DATABASE`, `USER`, i `PASSWORD` stałe w kodzie hello i Zastąp hello przykładowe wartości z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c793f-156">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span> 
4. <span data-ttu-id="c793f-157">Uruchom wiersz polecenia hello lub powłoki bash.</span><span class="sxs-lookup"><span data-stu-id="c793f-157">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="c793f-158">Przejdź do folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="c793f-158">Change directory into your project folder.</span></span> <span data-ttu-id="c793f-159">Na przykład w systemie Windows uruchom polecenie `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="c793f-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="c793f-160">W systemie Linux: `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="c793f-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="c793f-161">Niektóre z wymienionych edytory IDE hello oferują możliwości debugowania i środowiska uruchomieniowego bez konieczności poleceń powłoki.</span><span class="sxs-lookup"><span data-stu-id="c793f-161">Some of hello IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="c793f-162">Uruchom kod hello, wpisując polecenie hello `go run createtable.go` toocompile hello aplikacji i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="c793f-162">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="c793f-163">Alternatywnie toobuild hello kodu do natywnej aplikacji, `go build createtable.go`, uruchom `createtable.exe` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c793f-163">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="c793f-164">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="c793f-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="c793f-165">Użyj następujących hello kodu serwera toohello tooconnect, Utwórz tabelę i załadować hello danych przy użyciu **Wstaw** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c793f-165">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="c793f-166">Kod Hello importuje trzy pakiety: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [sterownik Przejdź sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) jako toocommunicate sterowników, z hello Azure bazy danych MySQL i hello [formatowaniu pakietu](https://golang.org/pkg/fmt/)dla drukowanej dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-166">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="c793f-167">Witaj kod wywołuje metodę [sql. Metody Open()](http://go-database-sql.org/accessing.html) tooAzure tooconnect bazy danych MySQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="c793f-167">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="c793f-168">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c793f-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="c793f-169">Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) metody toorun kilka razy niektóre polecenia języka DDL.</span><span class="sxs-lookup"><span data-stu-id="c793f-169">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several DDL commands.</span></span> <span data-ttu-id="c793f-170">Kod Hello używa również hello [Prepare()](http://go-database-sql.org/prepared.html) i Exec() toorun przygotowane instrukcje o innych parametrach tooinsert trzech wierszy.</span><span class="sxs-lookup"><span data-stu-id="c793f-170">hello code also uses hello [Prepare()](http://go-database-sql.org/prepared.html) and Exec() toorun prepared statements with different parameters tooinsert three rows.</span></span> <span data-ttu-id="c793f-171">Zawsze metody checkError() niestandardowy jest toocheck używane, jeśli wystąpił błąd i awaryjne tooexit.</span><span class="sxs-lookup"><span data-stu-id="c793f-171">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="c793f-172">Zastąp hello `host`, `database`, `user`, i `password` stałe z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c793f-172">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a><span data-ttu-id="c793f-173">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="c793f-173">Read data</span></span>
<span data-ttu-id="c793f-174">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c793f-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="c793f-175">Kod Hello importuje trzy pakiety: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [sterownik Przejdź sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) jako toocommunicate sterowników, z hello Azure bazy danych MySQL i hello [formatowaniu pakietu](https://golang.org/pkg/fmt/)dla drukowanej dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="c793f-176">Witaj kod wywołuje metodę [sql. Metody Open()](http://go-database-sql.org/accessing.html) tooAzure tooconnect bazy danych MySQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="c793f-176">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="c793f-177">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c793f-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="c793f-178">Witaj Witaj wywołań kodu [Query()](https://golang.org/pkg/database/sql/#DB.Query) polecenia wyboru hello toorun metody.</span><span class="sxs-lookup"><span data-stu-id="c793f-178">hello code calls hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) method toorun hello select command.</span></span> <span data-ttu-id="c793f-179">Następnie uruchomieniu [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate za pomocą zestawu wyników hello i [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello wartości w kolumnie, zapisywanie hello wartości do zmiennych.</span><span class="sxs-lookup"><span data-stu-id="c793f-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate through hello result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello column values, saving hello value into variables.</span></span> <span data-ttu-id="c793f-180">Zawsze metody checkError() niestandardowy jest toocheck używane, jeśli wystąpił błąd i awaryjne tooexit.</span><span class="sxs-lookup"><span data-stu-id="c793f-180">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="c793f-181">Zastąp hello `host`, `database`, `user`, i `password` stałe z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c793f-181">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a><span data-ttu-id="c793f-182">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="c793f-182">Update data</span></span>
<span data-ttu-id="c793f-183">Użyj hello następujący kod tooconnect i zaktualizować hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c793f-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="c793f-184">Kod Hello importuje trzy pakiety: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [sterownik Przejdź sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) jako toocommunicate sterowników, z hello Azure bazy danych MySQL i hello [formatowaniu pakietu](https://golang.org/pkg/fmt/)dla drukowanej dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="c793f-185">Witaj kod wywołuje metodę [sql. Metody Open()](http://go-database-sql.org/accessing.html) tooAzure tooconnect bazy danych MySQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="c793f-185">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="c793f-186">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c793f-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="c793f-187">Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) polecenia update hello toorun metody.</span><span class="sxs-lookup"><span data-stu-id="c793f-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello update command.</span></span> <span data-ttu-id="c793f-188">Zawsze metody checkError() niestandardowy jest toocheck używane, jeśli wystąpił błąd i awaryjne tooexit.</span><span class="sxs-lookup"><span data-stu-id="c793f-188">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="c793f-189">Zastąp hello `host`, `database`, `user`, i `password` stałe z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c793f-189">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="c793f-190">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="c793f-190">Delete data</span></span>
<span data-ttu-id="c793f-191">Użyj hello następujący kod tooconnect i usuwanie danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="c793f-191">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="c793f-192">Kod Hello importuje trzy pakiety: hello [pakietu sql](https://golang.org/pkg/database/sql/), hello [sterownik Przejdź sql dla programu mysql](https://github.com/go-sql-driver/mysql#installation) jako toocommunicate sterowników, z hello Azure bazy danych MySQL i hello [formatowaniu pakietu](https://golang.org/pkg/fmt/)dla drukowanej dane wejściowe i wyjściowe hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="c793f-193">Witaj kod wywołuje metodę [sql. Metody Open()](http://go-database-sql.org/accessing.html) tooAzure tooconnect bazy danych MySQL i kontroli hello połączenie za pomocą metody [bazy danych. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="c793f-193">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="c793f-194">A [dojście do bazy danych](https://golang.org/pkg/database/sql/#DB) jest używana w całym, zawierający puli połączeń hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c793f-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="c793f-195">Witaj Witaj wywołań kodu [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun metody Usuwanie polecenia.</span><span class="sxs-lookup"><span data-stu-id="c793f-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello delete command.</span></span> <span data-ttu-id="c793f-196">Zawsze metody checkError() niestandardowy jest toocheck używane, jeśli wystąpił błąd i awaryjne tooexit.</span><span class="sxs-lookup"><span data-stu-id="c793f-196">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="c793f-197">Zastąp hello `host`, `database`, `user`, i `password` stałe z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c793f-197">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="c793f-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c793f-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c793f-199">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="c793f-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
