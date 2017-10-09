---
title: "Połącz tooAzure bazy danych dla programu MySQL z C++ | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera przykładowy kod C++ można użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="608cc-103">Bazy danych platformy Azure dla programu MySQL: dane tooconnect i zapytań Użyj łącznika/C++</span><span class="sxs-lookup"><span data-stu-id="608cc-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="608cc-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu aplikacji C++.</span><span class="sxs-lookup"><span data-stu-id="608cc-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="608cc-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="608cc-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="608cc-106">Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu języka C++ oraz czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="608cc-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="608cc-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="608cc-107">Prerequisites</span></span>
<span data-ttu-id="608cc-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="608cc-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="608cc-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="608cc-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="608cc-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="608cc-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="608cc-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="608cc-111">You also need to:</span></span>
- <span data-ttu-id="608cc-112">Zainstalować program [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="608cc-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="608cc-113">Zainstalować program [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="608cc-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="608cc-114">Zainstalować [łącznik bazy danych MySQL/środowisko C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="608cc-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="608cc-115">Zainstalować rozwiązanie [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="608cc-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="608cc-116">Instalowanie programu Visual Studio i technologii .NET</span><span class="sxs-lookup"><span data-stu-id="608cc-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="608cc-117">kroki Hello w tej sekcji założono, że znasz tworzenie przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="608cc-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="608cc-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="608cc-118">**Windows**</span></span>
1. <span data-ttu-id="608cc-119">Zainstaluj program Visual Studio 2017 Community — wyposażone w pełen zestaw funkcji, rozszerzalne, bezpłatne środowisko IDE do tworzenia nowoczesnych aplikacji przeznaczonych dla systemów Android, iOS, Windows, a także aplikacji internetowych, aplikacji baz danych oraz usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="608cc-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="608cc-120">Można zainstalować hello pełne .NET Framework albo właśnie .NET Core.</span><span class="sxs-lookup"><span data-stu-id="608cc-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="608cc-121">wstawki kodu Hello w hello Szybki Start pracy z jednym.</span><span class="sxs-lookup"><span data-stu-id="608cc-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="608cc-122">Jeśli masz już Visual Studio na komputerze jest zainstalowany, Pomiń hello następne dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="608cc-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="608cc-123">Pobierz hello [Instalator Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="608cc-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="608cc-124">Uruchom Instalator hello i wykonaj hello instalacji monity toocomplete hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="608cc-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="608cc-125">**Konfigurowanie programu Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="608cc-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="608cc-126">W programie Visual Studio projektu właściwości > Właściwości konfiguracji > C/C++ > konsolidatora > Ogólne > katalogi dodatkowych bibliotek, Dodaj katalog lib\opt hello (np.: C:\Program Files (x86) \MySQL\MySQL C++ łącznika 1.1.9\lib\opt) z hello c ++ Łącznik.</span><span class="sxs-lookup"><span data-stu-id="608cc-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="608cc-127">W programie Visual Studio wybierz kolejno pozycje Właściwość projektu > Właściwości konfiguracji > C/C++ > Ogólne > Dodatkowe katalogi dyrektywy include</span><span class="sxs-lookup"><span data-stu-id="608cc-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="608cc-128">Dodaj katalog include/ łącznika języka C++ (tj. C:\Program Files (x86) \MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="608cc-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="608cc-129">Dodaj katalog główny biblioteki Boost (tj. C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="608cc-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="608cc-130">W programie Visual Studio projektu właściwości > Właściwości konfiguracji > C/C++ > konsolidatora > wprowadzania > istnieją dodatkowe zależności, Dodaj mysqlcppconn.lib do pola tekstowego hello</span><span class="sxs-lookup"><span data-stu-id="608cc-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="608cc-131">Albo mysqlcppconn.dll kopiowania z hello c ++ łącznika folder biblioteki w kroku 3 toohello tym samym katalogu co plik wykonywalny aplikacji hello lub dodać toohello zmiennej środowiskowej, można odnaleźć aplikacji.</span><span class="sxs-lookup"><span data-stu-id="608cc-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="608cc-132">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="608cc-132">Get connection information</span></span>
<span data-ttu-id="608cc-133">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="608cc-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="608cc-134">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="608cc-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="608cc-135">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="608cc-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="608cc-136">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="608cc-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="608cc-137">Kliknij nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="608cc-137">Click hello server name.</span></span>
4. <span data-ttu-id="608cc-138">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="608cc-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="608cc-139">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="608cc-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="608cc-140">![Nazwa serwera usługi Azure Database for MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="608cc-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="608cc-141">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="608cc-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="608cc-142">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="608cc-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="608cc-143">Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="608cc-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="608cc-144">Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="608cc-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="608cc-145">Następnie hello kod używa metody createStatement() i metody execute() toorun hello bazy danych poleceń.</span><span class="sxs-lookup"><span data-stu-id="608cc-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="608cc-146">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="608cc-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="608cc-147">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="608cc-147">Read data</span></span>

<span data-ttu-id="608cc-148">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="608cc-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="608cc-149">Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="608cc-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="608cc-150">Następnie hello kod używa metody prepareStatement() i executeQuery() toorun hello wybierz polecenia.</span><span class="sxs-lookup"><span data-stu-id="608cc-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="608cc-151">Na koniec hello kodzie użyto next() tooadvance toohello rekordów w wynikach hello.</span><span class="sxs-lookup"><span data-stu-id="608cc-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="608cc-152">Następnie kod hello używa wartości hello tooparse getInt() i getString() w rekordzie hello.</span><span class="sxs-lookup"><span data-stu-id="608cc-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="608cc-153">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="608cc-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="608cc-154">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="608cc-154">Update data</span></span>
<span data-ttu-id="608cc-155">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="608cc-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="608cc-156">Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="608cc-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="608cc-157">Następnie hello kod używa metody prepareStatement() i executeQuery() toorun hello polecenia aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="608cc-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="608cc-158">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="608cc-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="608cc-159">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="608cc-159">Delete data</span></span>
<span data-ttu-id="608cc-160">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="608cc-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="608cc-161">Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="608cc-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="608cc-162">Następnie hello kod używa metody prepareStatement() i executeQuery() toorun hello Usuń poleceń.</span><span class="sxs-lookup"><span data-stu-id="608cc-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="608cc-163">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="608cc-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="608cc-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="608cc-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="608cc-165">Migrowanie tooAzure bazy danych programu MySQL bazy danych dla programu MySQL przy użyciu zrzutu i przywracania</span><span class="sxs-lookup"><span data-stu-id="608cc-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
