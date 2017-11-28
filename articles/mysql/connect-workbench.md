---
title: "Połącz tooAzure bazy danych dla programu MySQL z MySQL Workbench | Dokumentacja firmy Microsoft"
description: "Tego przewodnika Szybki Start zawiera toouse kroki hello MySQL Workbench tooconnect i zapytań dane z bazy danych Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="ae00c-103">Bazy danych platformy Azure dla programu MySQL: Użyj MySQL Workbench danych tooconnect i zapytań</span><span class="sxs-lookup"><span data-stu-id="ae00c-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="ae00c-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL używania hello aplikacja MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="ae00c-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ae00c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ae00c-105">Prerequisites</span></span>
<span data-ttu-id="ae00c-106">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="ae00c-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="ae00c-107">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae00c-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="ae00c-108">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ae00c-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="ae00c-109">Zainstaluj narzędzia Workbench MySQL</span><span class="sxs-lookup"><span data-stu-id="ae00c-109">Install MySQL Workbench</span></span>
<span data-ttu-id="ae00c-110">Pobierz i zainstaluj MySQL Workbench na komputerze z [hello MySQL witryny sieci Web](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="ae00c-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ae00c-111">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="ae00c-111">Get connection information</span></span>
<span data-ttu-id="ae00c-112">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="ae00c-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="ae00c-113">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="ae00c-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ae00c-114">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ae00c-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="ae00c-115">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="ae00c-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="ae00c-116">Kliknij nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="ae00c-116">Click hello server name.</span></span>

4. <span data-ttu-id="ae00c-117">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="ae00c-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="ae00c-118">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="ae00c-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Bazy danych platformy Azure dla nazwy serwera MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="ae00c-120">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="ae00c-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="ae00c-121">Połącz serwer toohello przy użyciu narzędzia MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="ae00c-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="ae00c-122">za pomocą hello graficznego interfejsu użytkownika narzędzia MySQL Workbench serwer MySQL tooAzure tooconnect:</span><span class="sxs-lookup"><span data-stu-id="ae00c-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="ae00c-123">Uruchom program hello MySQL Workbench aplikacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="ae00c-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="ae00c-124">W **instalacji nowego połączenia** okna dialogowego wprowadź następujące informacje na powitania hello **parametry** karty:</span><span class="sxs-lookup"><span data-stu-id="ae00c-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![konfigurowanie nowego połączenia](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="ae00c-126">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="ae00c-126">**Setting**</span></span> | <span data-ttu-id="ae00c-127">**Sugerowana wartość**</span><span class="sxs-lookup"><span data-stu-id="ae00c-127">**Suggested value**</span></span> | <span data-ttu-id="ae00c-128">**Opis pola**</span><span class="sxs-lookup"><span data-stu-id="ae00c-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="ae00c-129">Nazwa połączenia</span><span class="sxs-lookup"><span data-stu-id="ae00c-129">Connection Name</span></span> | <span data-ttu-id="ae00c-130">Połączenie demonstracyjne</span><span class="sxs-lookup"><span data-stu-id="ae00c-130">Demo Connection</span></span> | <span data-ttu-id="ae00c-131">Podaj etykietę dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="ae00c-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="ae00c-132">Metoda połączenia</span><span class="sxs-lookup"><span data-stu-id="ae00c-132">Connection Method</span></span> | <span data-ttu-id="ae00c-133">Standardowa (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="ae00c-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="ae00c-134">Metoda Standardowa (TCP/IP) jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="ae00c-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="ae00c-135">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="ae00c-135">Hostname</span></span> | <span data-ttu-id="ae00c-136">*nazwa serwera*</span><span class="sxs-lookup"><span data-stu-id="ae00c-136">*server name*</span></span> | <span data-ttu-id="ae00c-137">Określ wartość hello nazwy serwera, który został użyty podczas hello Azure bazy danych dla programu MySQL wcześniej utworzony.</span><span class="sxs-lookup"><span data-stu-id="ae00c-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ae00c-138">Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj hello pełną nazwę domeny (\*. mysql.database.azure.com) jak pokazano w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="ae00c-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="ae00c-139">Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="ae00c-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="ae00c-140">Port</span><span class="sxs-lookup"><span data-stu-id="ae00c-140">Port</span></span> | <span data-ttu-id="ae00c-141">3306</span><span class="sxs-lookup"><span data-stu-id="ae00c-141">3306</span></span> | <span data-ttu-id="ae00c-142">Należy zawsze używać portu 3306 podczas łączenia tooAzure bazy danych dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="ae00c-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="ae00c-143">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="ae00c-143">Username</span></span> |  <span data-ttu-id="ae00c-144">*nazwa logowania administratora serwera*</span><span class="sxs-lookup"><span data-stu-id="ae00c-144">*server admin login name*</span></span> | <span data-ttu-id="ae00c-145">Wpisz powitania serwera admin logowania użytkownika dostarczana, gdy dla programu MySQL utworzony wcześniej hello bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="ae00c-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ae00c-146">Przykładowa nazwa użytkownika to myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="ae00c-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="ae00c-147">Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae00c-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="ae00c-148">Hello format jest  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="ae00c-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="ae00c-149">Hasło</span><span class="sxs-lookup"><span data-stu-id="ae00c-149">Password</span></span> | <span data-ttu-id="ae00c-150">Twoje hasło</span><span class="sxs-lookup"><span data-stu-id="ae00c-150">your password</span></span> | <span data-ttu-id="ae00c-151">Kliknij przycisk **magazynu w magazynie...**  przycisk toosave hello hasła.</span><span class="sxs-lookup"><span data-stu-id="ae00c-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="ae00c-152">Kliknij przycisk **Testuj połączenie** tootest, jeśli wszystkie parametry są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="ae00c-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="ae00c-153">Kliknij przycisk **OK** toosave hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="ae00c-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="ae00c-154">W hello lista **połączeń MySQL**, kliknij odpowiedni serwer tooyour hello kafelków i poczekaj, aż hello toobe połączenie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="ae00c-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="ae00c-155">Otwiera nową kartę SQL za pomocą edytora puste można wpisać zapytań.</span><span class="sxs-lookup"><span data-stu-id="ae00c-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae00c-156">Domyślnie zabezpieczeń połączenia SSL jest wymagany i wymuszane MySQL serwera bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="ae00c-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="ae00c-157">Zwykle nie jest dodatkowa konfiguracja certyfikatów SSL wymagane dla serwera tooyour tooconnect MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="ae00c-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="ae00c-158">Aby uzyskać więcej informacji dotyczących protokołu SSL, zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ae00c-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="ae00c-159">Toodisable protokołu SSL, należy odwiedzić hello portalu Azure i przycisk hello połączenia zabezpieczeń strony toodisable hello Wymuszanie protokołu SSL połączenia przełącznika.</span><span class="sxs-lookup"><span data-stu-id="ae00c-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="ae00c-160">Utwórz tabelę, wstawiania danych, odczytywanie danych, aktualizowanie danych i usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="ae00c-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="ae00c-161">Skopiuj i Wklej hello przykładowy kod SQL w puste tooillustrate kartę SQL przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="ae00c-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="ae00c-162">Ten kod tworzy pustą bazę danych o nazwie quickstartdb, a następnie tworzy Przykładowa tabela o nazwie spisu.</span><span class="sxs-lookup"><span data-stu-id="ae00c-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="ae00c-163">Wstawia niektórych wierszy następnie odczytuje hello wierszy.</span><span class="sxs-lookup"><span data-stu-id="ae00c-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="ae00c-164">Zmienia hello danych za pomocą instrukcji update i odczytuje Witaj ponownie wierszy.</span><span class="sxs-lookup"><span data-stu-id="ae00c-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="ae00c-165">Na koniec go usuwa wiersz i odczytuje wierszy hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="ae00c-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="ae00c-166">Hello zrzut ekranu przedstawia przykład hello kod SQL w danych wyjściowych SQL Workbench i hello, po jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="ae00c-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![Kod SQL próbki toorun karcie SQL Workbench MySQL](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="ae00c-168">toorun hello przykładowy kod SQL, kliknij przycisk hello rozjaśnienie ikonę w pasku narzędzi hello hello **pliku SQL** kartę.</span><span class="sxs-lookup"><span data-stu-id="ae00c-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="ae00c-169">Zwróć uwagę, hello trzech wyników z kartami w hello **Siatka wyników** sekcji w środku hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ae00c-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="ae00c-170">Powiadomienie hello **dane wyjściowe** listy u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ae00c-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="ae00c-171">zostanie wyświetlony stan Hello każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ae00c-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="ae00c-172">Teraz połączyły tooAzure bazy danych dla programu MySQL przy użyciu narzędzia MySQL Workbench i wykonano zapytanie danych przy użyciu języka SQL hello.</span><span class="sxs-lookup"><span data-stu-id="ae00c-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae00c-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae00c-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ae00c-174">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="ae00c-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
