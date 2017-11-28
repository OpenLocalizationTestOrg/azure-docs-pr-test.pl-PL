---
title: "VS Code: nawiązywanie połączenia i wykonywanie zapytań dotyczących danych w bazie danych Azure SQL Database | Microsoft Docs"
description: "Dowiedz się, jak tooconnect tooSQL bazy danych na platformie Azure przy użyciu programu Visual Studio Code. Następnie uruchom instrukcji języka Transact-SQL (T-SQL) tooquery i edytowanie danych."
metacanonical: 
keywords: "Połącz toosql bazy danych"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a><span data-ttu-id="767fa-105">Baza danych SQL Azure: Użyj Visual Studio Code tooconnect i zapytań danych</span><span class="sxs-lookup"><span data-stu-id="767fa-105">Azure SQL Database: Use Visual Studio Code tooconnect and query data</span></span>

<span data-ttu-id="767fa-106">[Visual Studio Code](https://code.visualstudio.com/docs) to edytor graficzny kodu dla systemu Linux, macOS, i systemu Windows, które obsługuje rozszerzenia, w tym hello [rozszerzenia mssql](https://aka.ms/mssql-marketplace) do wykonywania zapytań programu Microsoft SQL Server, bazy danych SQL Azure i SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="767fa-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="767fa-107">To szybki start pokazuje, jak baza danych Azure SQL tooan toouse Visual Studio Code tooconnect, a następnie tooquery instrukcje użycia języka Transact-SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-107">This quick start demonstrates how toouse Visual Studio Code tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="767fa-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="767fa-108">Prerequisites</span></span>

<span data-ttu-id="767fa-109">To szybki start używa jako początkowy punkt zasobów hello tworzony w jednej z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="767fa-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="767fa-110">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="767fa-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="767fa-111">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="767fa-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="767fa-112">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="767fa-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="767fa-113">Przed rozpoczęciem upewnij się, zainstalowano hello najnowsza wersja [Visual Studio Code](https://code.visualstudio.com/Download) i załadować hello [rozszerzenia mssql](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="767fa-113">Before you start, make sure you have installed hello newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded hello [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="767fa-114">Aby instalacja rozszerzenia mssql hello, zobacz [Zainstaluj kod programu VS](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) i zobacz [mssql dla programu Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="767fa-114">For installation guidance for hello mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="767fa-115">Konfigurowanie kodu programu VS</span><span class="sxs-lookup"><span data-stu-id="767fa-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="767fa-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="767fa-116">**Mac OS**</span></span>
<span data-ttu-id="767fa-117">System macOS należy tooinstall biblioteki OpenSSL, które jest wymagań wstępnych dla podstawowej platformy DotNet rozszerzenie tego mssql używa.</span><span class="sxs-lookup"><span data-stu-id="767fa-117">For macOS, you need tooinstall OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="767fa-118">Otwórz terminala i wprowadź następujące polecenia tooinstall hello **brew** i **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="767fa-118">Open your terminal and enter hello following commands tooinstall **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="767fa-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="767fa-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="767fa-120">Nie jest potrzebna specjalna konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="767fa-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="767fa-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="767fa-121">**Windows**</span></span>

<span data-ttu-id="767fa-122">Nie jest potrzebna specjalna konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="767fa-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="767fa-123">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="767fa-123">SQL server connection information</span></span>

<span data-ttu-id="767fa-124">Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="767fa-124">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="767fa-125">Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.</span><span class="sxs-lookup"><span data-stu-id="767fa-125">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="767fa-126">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="767fa-126">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="767fa-127">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="767fa-127">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="767fa-128">Na powitania **omówienie** stron dla bazy danych, przejrzyj hello w pełni kwalifikowana nazwa serwera, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="767fa-128">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="767fa-129">Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.</span><span class="sxs-lookup"><span data-stu-id="767fa-129">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![informacje o połączeniu](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="767fa-131">Jeśli pamiętasz hello informacje logowania dla serwera bazy danych SQL Azure, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera i, w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-131">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="set-language-mode-toosql"></a><span data-ttu-id="767fa-132">TooSQL tryb języka zestawu</span><span class="sxs-lookup"><span data-stu-id="767fa-132">Set language mode tooSQL</span></span>

<span data-ttu-id="767fa-133">Ustaw tryb języka hello ustawiono zbyt**SQL** w programie Visual Studio Code tooenable mssql poleceń i IntelliSense T-SQL.</span><span class="sxs-lookup"><span data-stu-id="767fa-133">Set hello language mode is set too**SQL** in Visual Studio Code tooenable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="767fa-134">Otwórz nowe okno programu Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="767fa-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="767fa-135">Kliknij przycisk **zwykły tekst** w hello prawym dolnym rogu paska stanu hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-135">Click **Plain Text** in hello lower right-hand corner of hello status bar.</span></span>
3. <span data-ttu-id="767fa-136">W hello **tryb wybrany język** menu rozwijanego, który zostanie otwarty, typ **SQL**, a następnie naciśnij klawisz **ENTER** tooset hello języka tryb tooSQL.</span><span class="sxs-lookup"><span data-stu-id="767fa-136">In hello **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** tooset hello language mode tooSQL.</span></span> 

   ![Tryb języka SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a><span data-ttu-id="767fa-138">Połącz tooyour bazy danych</span><span class="sxs-lookup"><span data-stu-id="767fa-138">Connect tooyour database</span></span>

<span data-ttu-id="767fa-139">Za pomocą programu Visual Studio Code tooestablish serwer bazy danych SQL Azure tooyour połączenia.</span><span class="sxs-lookup"><span data-stu-id="767fa-139">Use Visual Studio Code tooestablish a connection tooyour Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="767fa-140">Przed kontynuowaniem upewnij się, że masz przygotowany serwer, bazę danych i informacje logowania.</span><span class="sxs-lookup"><span data-stu-id="767fa-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="767fa-141">Po rozpoczęciu wprowadzania informacji o profilu połączenia hello, jeżeli zmienić fokus w Visual Studio Code, masz toorestart tworzenia profilu połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-141">Once you begin entering hello connection profile information, if you change your focus from Visual Studio Code, you have toorestart creating hello connection profile.</span></span>
>

1. <span data-ttu-id="767fa-142">W kodzie VS, naciśnij klawisz **CTRL + SHIFT + P** (lub **F1**) tooopen hello palety polecenia.</span><span class="sxs-lookup"><span data-stu-id="767fa-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) tooopen hello Command Palette.</span></span>

2. <span data-ttu-id="767fa-143">Wpisz **sqlcon** i naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="767fa-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="767fa-144">Naciśnij klawisz **ENTER** tooselect **Utwórz profil połączenia**.</span><span class="sxs-lookup"><span data-stu-id="767fa-144">Press **ENTER** tooselect **Create Connection Profile**.</span></span> <span data-ttu-id="767fa-145">W ten sposób zostanie utworzony profil połączenia dla wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="767fa-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="767fa-146">Wykonaj hello monity toospecify hello właściwości połączenia hello nowy profil połączenia.</span><span class="sxs-lookup"><span data-stu-id="767fa-146">Follow hello prompts toospecify hello connection properties for hello new connection profile.</span></span> <span data-ttu-id="767fa-147">Po określeniu każdej wartości, naciśnij klawisz **ENTER** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="767fa-147">After specifying each value, press **ENTER** toocontinue.</span></span> 

   | <span data-ttu-id="767fa-148">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="767fa-148">Setting</span></span>       | <span data-ttu-id="767fa-149">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="767fa-149">Suggested value</span></span> | <span data-ttu-id="767fa-150">Opis</span><span class="sxs-lookup"><span data-stu-id="767fa-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="767fa-151">**Nazwa serwera</span><span class="sxs-lookup"><span data-stu-id="767fa-151">**Server name</span></span> | <span data-ttu-id="767fa-152">Nazwa FQDN serwera Hello</span><span class="sxs-lookup"><span data-stu-id="767fa-152">hello fully qualified server name</span></span> | <span data-ttu-id="767fa-153">Witaj nazwa powinna być podobny do następującego: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="767fa-153">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="767fa-154">**Nazwa bazy danych**</span><span class="sxs-lookup"><span data-stu-id="767fa-154">**Database name**</span></span> | <span data-ttu-id="767fa-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="767fa-155">mySampleDatabase</span></span> | <span data-ttu-id="767fa-156">Nazwa Hello hello bazy danych toowhich tooconnect.</span><span class="sxs-lookup"><span data-stu-id="767fa-156">hello name of hello database toowhich tooconnect.</span></span> |
   | <span data-ttu-id="767fa-157">**Uwierzytelnianie**</span><span class="sxs-lookup"><span data-stu-id="767fa-157">**Authentication**</span></span> | <span data-ttu-id="767fa-158">Identyfikator logowania SQL</span><span class="sxs-lookup"><span data-stu-id="767fa-158">SQL Login</span></span>| <span data-ttu-id="767fa-159">Uwierzytelnianie programu SQL jest typ uwierzytelniania tylko hello ma został skonfigurowany w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="767fa-159">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="767fa-160">**Nazwa użytkownika**</span><span class="sxs-lookup"><span data-stu-id="767fa-160">**User name**</span></span> | <span data-ttu-id="767fa-161">konto administratora powitania serwera</span><span class="sxs-lookup"><span data-stu-id="767fa-161">hello server admin account</span></span> | <span data-ttu-id="767fa-162">To konto hello określone podczas tworzenia powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="767fa-162">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="767fa-163">**Hasło (identyfikator logowania SQL)**</span><span class="sxs-lookup"><span data-stu-id="767fa-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="767fa-164">Witaj hasło do konta administratora serwera</span><span class="sxs-lookup"><span data-stu-id="767fa-164">hello password for your server admin account</span></span> | <span data-ttu-id="767fa-165">Jest to hasło hello określone podczas tworzenia powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="767fa-165">This is hello password that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="767fa-166">**Zapisać hasło?**</span><span class="sxs-lookup"><span data-stu-id="767fa-166">**Save Password?**</span></span> | <span data-ttu-id="767fa-167">Tak lub Nie</span><span class="sxs-lookup"><span data-stu-id="767fa-167">Yes or No</span></span> | <span data-ttu-id="767fa-168">Wybierz opcję Tak, jeśli nie chcesz tooenter hello hasła zawsze.</span><span class="sxs-lookup"><span data-stu-id="767fa-168">Select Yes if you do not want tooenter hello password each time.</span></span> |
   | <span data-ttu-id="767fa-169">**Wprowadź nazwę dla tego profilu**</span><span class="sxs-lookup"><span data-stu-id="767fa-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="767fa-170">Nazwa profilu, np. **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="767fa-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="767fa-171">Zapisana nazwa profilu przyspiesza połączenie podczas kolejnych logowań.</span><span class="sxs-lookup"><span data-stu-id="767fa-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="767fa-172">Naciśnij klawisz hello **ESC** klucza tooclose hello komunikat z informacjami o informujące, że profil hello jest utworzone i połączone.</span><span class="sxs-lookup"><span data-stu-id="767fa-172">Press hello **ESC** key tooclose hello info message that informs you that hello profile is created and connected.</span></span>

6. <span data-ttu-id="767fa-173">Sprawdź połączenie na pasku stanu hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-173">Verify your connection in hello status bar.</span></span>

   ![Stan połączenia](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="767fa-175">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="767fa-175">Query data</span></span>

<span data-ttu-id="767fa-176">Użyj hello poniższy kod tooquery produktów pierwsza 20. wg hello według kategorii przy użyciu hello [wybierz](https://msdn.microsoft.com/library/ms189499.aspx) instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="767fa-176">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="767fa-177">W hello **edytor** okna, wprowadź następujące zapytanie w oknie zapytania pusty hello hello:</span><span class="sxs-lookup"><span data-stu-id="767fa-177">In hello **Editor** window, enter hello following query in hello empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="767fa-178">Naciśnij klawisz **CTRL + SHIFT + E** tooretrieve danych z tabel hello produktu i ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="767fa-178">Press **CTRL+SHIFT+E** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![Zapytanie](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="767fa-180">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="767fa-180">Insert data</span></span>

<span data-ttu-id="767fa-181">Poniższy hello używany kod tooinsert nowego produktu do hello SalesLT.Product tabeli hello [Wstaw](https://msdn.microsoft.com/library/ms174335.aspx) instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="767fa-181">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="767fa-182">W hello **edytor** okna, Usuń poprzednie zapytanie hello i wprowadź hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="767fa-182">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="767fa-183">Naciśnij klawisz **CTRL + SHIFT + E** tooinsert nowy wiersz w tabeli produktu hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-183">Press **CTRL+SHIFT+E** tooinsert a new row in hello Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="767fa-184">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="767fa-184">Update data</span></span>

<span data-ttu-id="767fa-185">Użyj hello poniższy kod tooupdate hello nowego produktu czy wcześniej dodane za pomocą hello [aktualizacji](https://msdn.microsoft.com/library/ms177523.aspx) instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="767fa-185">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="767fa-186">W hello **edytor** okna, Usuń poprzednie zapytanie hello i wprowadź hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="767fa-186">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="767fa-187">Naciśnij klawisz **CTRL + SHIFT + E** tooupdate hello określony wiersz w tabeli produktu hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-187">Press **CTRL+SHIFT+E** tooupdate hello specified row in hello Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="767fa-188">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="767fa-188">Delete data</span></span>

<span data-ttu-id="767fa-189">Użyj hello poniższy kod toodelete hello nowego produktu czy wcześniej dodane za pomocą hello [usunąć](https://msdn.microsoft.com/library/ms189835.aspx) instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="767fa-189">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="767fa-190">W hello **edytor** okna, Usuń poprzednie zapytanie hello i wprowadź hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="767fa-190">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="767fa-191">Naciśnij klawisz **CTRL + SHIFT + E** toodelete hello określony wiersz w tabeli produktu hello.</span><span class="sxs-lookup"><span data-stu-id="767fa-191">Press **CTRL+SHIFT+E** toodelete hello specified row in hello Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="767fa-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="767fa-192">Next steps</span></span>

- <span data-ttu-id="767fa-193">tooconnect i zapytania za pomocą programu SQL Server Management Studio, zobacz [Connect i zapytanie z SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="767fa-193">tooconnect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="767fa-194">Aby zapoznać się z artykułem w magazynie MSDN dotyczącym programu Visual Studio Code, zobacz temat [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115) (Tworzenie bazy danych w środowisku IDE, korzystając z wpisu na blogu dotyczącym rozszerzenia MSSQL).</span><span class="sxs-lookup"><span data-stu-id="767fa-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
