---
title: "Nawiązywanie połączeń z usługą Azure Database for MySQL za pomocą języka C++ | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera przykład kodu w języku C++, za pomocą którego można nawiązywać połączenie z danymi usługi Azure Database for MySQL i wykonywać zapytania względem nich."
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
ms.openlocfilehash: 63388b83b913d95136140fa4c56af0dbebbdad81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="d6a3a-103">Usługa Azure Database for MySQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań przy użyciu łącznika/języka C++</span><span class="sxs-lookup"><span data-stu-id="d6a3a-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="d6a3a-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for MySQL przy użyciu aplikacji języka C++.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="d6a3a-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="d6a3a-106">W krokach w tym artykule założono, że wiesz już, jak opracowywać zawartość za pomocą języka C++, i dopiero zaczynasz pracę z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-106">The steps in this article assume that you are familiar with developing using C++, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6a3a-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d6a3a-107">Prerequisites</span></span>
<span data-ttu-id="d6a3a-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="d6a3a-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d6a3a-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d6a3a-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="d6a3a-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6a3a-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="d6a3a-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="d6a3a-111">You also need to:</span></span>
- <span data-ttu-id="d6a3a-112">Zainstalować program [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="d6a3a-113">Zainstalować program [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="d6a3a-114">Zainstalować [łącznik bazy danych MySQL/środowisko C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="d6a3a-115">Zainstalować rozwiązanie [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="d6a3a-116">Instalowanie programu Visual Studio i technologii .NET</span><span class="sxs-lookup"><span data-stu-id="d6a3a-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="d6a3a-117">W krokach w tej sekcji założono, że wiesz już, jak programować za pomocą technologii .NET.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="d6a3a-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d6a3a-118">**Windows**</span></span>
1. <span data-ttu-id="d6a3a-119">Zainstaluj program Visual Studio 2017 Community — wyposażone w pełen zestaw funkcji, rozszerzalne, bezpłatne środowisko IDE do tworzenia nowoczesnych aplikacji przeznaczonych dla systemów Android, iOS, Windows, a także aplikacji internetowych, aplikacji baz danych oraz usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="d6a3a-120">Można zainstalować pełny program .NET Framework lub tylko program .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-120">You can install either the full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="d6a3a-121">Fragmenty kodu w tym przewodniku Szybki start współdziałają z oboma tymi programami.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-121">The code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="d6a3a-122">Jeśli na maszynie zainstalowano już program Visual Studio, pomiń dwa następne kroki.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-122">If you already have Visual Studio installed on your machine, skip the next two steps.</span></span>
   - <span data-ttu-id="d6a3a-123">Pobierz [Instalator programu Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="d6a3a-123">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="d6a3a-124">Uruchom instalatora i postępuj zgodnie z wyświetlanymi monitami, aby ukończyć instalację.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-124">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="d6a3a-125">**Konfigurowanie programu Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="d6a3a-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="d6a3a-126">W programie Visual Studio w lokalizacji Właściwość projektu > Właściwości konfiguracji > C/C++ > Konsolidator > Ogólne > Dodatkowe katalogi biblioteki dodaj katalog lib\opt (tj. C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) łącznika języka C++.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add the lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the c++ connector.</span></span>
2. <span data-ttu-id="d6a3a-127">W programie Visual Studio wybierz kolejno pozycje Właściwość projektu > Właściwości konfiguracji > C/C++ > Ogólne > Dodatkowe katalogi dyrektywy include</span><span class="sxs-lookup"><span data-stu-id="d6a3a-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="d6a3a-128">Dodaj katalog include/ łącznika języka C++ (tj. C:\Program Files (x86) \MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="d6a3a-129">Dodaj katalog główny biblioteki Boost (tj. C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="d6a3a-130">W programie Visual Studio w lokalizacji Właściwość projektu > Właściwości konfiguracji > C/C++ > Konsolidator > Wejście > Dodatkowe zależności dodaj plik mysqlcppconn.lib w polu tekstowym</span><span class="sxs-lookup"><span data-stu-id="d6a3a-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into the text field</span></span>
4. <span data-ttu-id="d6a3a-131">Skopiuj plik mysqlcppconn.dll z folderu biblioteki łącznika języka C++ utworzonego w kroku 3 do tego samego katalogu, w którym znajduje się plik wykonywalny aplikacji, albo dodaj go do zmiennej środowiskowej, aby aplikacja mogła go odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-131">Either copy mysqlcppconn.dll from the c++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d6a3a-132">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="d6a3a-132">Get connection information</span></span>
<span data-ttu-id="d6a3a-133">Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="d6a3a-134">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d6a3a-135">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6a3a-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d6a3a-136">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-136">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="d6a3a-137">Kliknij nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-137">Click the server name.</span></span>
4. <span data-ttu-id="d6a3a-138">Wybierz stronę **Właściwości** serwera.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="d6a3a-139">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d6a3a-140">![Nazwa serwera usługi Azure Database for MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="d6a3a-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="d6a3a-141">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d6a3a-142">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="d6a3a-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="d6a3a-143">Użyj poniższego kodu, aby nawiązać połączenie i załadować dane przy użyciu instrukcji **CREATE TABLE** i **INSERT INTO** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-143">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="d6a3a-144">Kod używa klasy sql::Driver z metodą connect() w celu ustanowienia połączenia z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-144">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d6a3a-145">Następnie kod używa metod createStatement() i execute(), aby uruchamiać polecenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-145">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="d6a3a-146">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-146">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
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

## <a name="read-data"></a><span data-ttu-id="d6a3a-147">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="d6a3a-147">Read data</span></span>

<span data-ttu-id="d6a3a-148">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-148">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="d6a3a-149">Kod używa klasy sql::Driver z metodą connect() w celu ustanowienia połączenia z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-149">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d6a3a-150">Następnie kod używa metod prepareStatement() i executeQuery(), aby uruchamiać polecenia select.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-150">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="d6a3a-151">Na końcu kod używa metody next() w celu przechodzenia do rekordów w wynikach.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-151">Finally the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="d6a3a-152">Następnie kod używa metod GetInt() i getString() w celu przeanalizowania wartości w rekordzie.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-152">Then the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="d6a3a-153">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
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

## <a name="update-data"></a><span data-ttu-id="d6a3a-154">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="d6a3a-154">Update data</span></span>
<span data-ttu-id="d6a3a-155">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-155">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="d6a3a-156">Kod używa klasy sql::Driver z metodą connect() w celu ustanowienia połączenia z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-156">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d6a3a-157">Następnie kod używa metod prepareStatement() i executeQuery(), aby uruchamiać polecenia update.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-157">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="d6a3a-158">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
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


## <a name="delete-data"></a><span data-ttu-id="d6a3a-159">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="d6a3a-159">Delete data</span></span>
<span data-ttu-id="d6a3a-160">Użyj poniższego kodu, aby nawiązać połączenie i odczytać dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-160">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="d6a3a-161">Kod używa klasy sql::Driver z metodą connect() w celu ustanowienia połączenia z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-161">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d6a3a-162">Następnie kod używa metod prepareStatement() i executeQuery(), aby uruchamiać polecenia delete.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-162">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="d6a3a-163">Zastąp parametry hosta, nazwy bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-163">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
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

## <a name="next-steps"></a><span data-ttu-id="d6a3a-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6a3a-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d6a3a-165">Migrowanie bazy danych MySQL do usługi Azure Database for MySQL przy użyciu zrzutu i przywracania</span><span class="sxs-lookup"><span data-stu-id="d6a3a-165">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
