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
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: dane tooconnect i zapytań Użyj łącznika/C++
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu aplikacji C++. Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello. Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu języka C++ oraz czy są nowe tooworking z bazą danych Azure dla programu MySQL.

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

Należy również:
- Zainstalować program [.NET Framework](https://www.microsoft.com/net/download)
- Zainstalować program [Visual Studio](https://www.visualstudio.com/downloads/)
- Zainstalować [łącznik bazy danych MySQL/środowisko C++](https://dev.mysql.com/downloads/connector/cpp/) 
- Zainstalować rozwiązanie [Boost](http://www.boost.org/)

## <a name="install-visual-studio-and-net"></a>Instalowanie programu Visual Studio i technologii .NET
kroki Hello w tej sekcji założono, że znasz tworzenie przy użyciu platformy .NET.

### <a name="windows"></a>**Windows**
1. Zainstaluj program Visual Studio 2017 Community — wyposażone w pełen zestaw funkcji, rozszerzalne, bezpłatne środowisko IDE do tworzenia nowoczesnych aplikacji przeznaczonych dla systemów Android, iOS, Windows, a także aplikacji internetowych, aplikacji baz danych oraz usług w chmurze. Można zainstalować hello pełne .NET Framework albo właśnie .NET Core. wstawki kodu Hello w hello Szybki Start pracy z jednym. Jeśli masz już Visual Studio na komputerze jest zainstalowany, Pomiń hello następne dwa kroki.
   - Pobierz hello [Instalator Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Uruchom Instalator hello i wykonaj hello instalacji monity toocomplete hello instalacji.

### <a name="configure-visual-studio"></a>**Konfigurowanie programu Visual Studio**
1. W programie Visual Studio projektu właściwości > Właściwości konfiguracji > C/C++ > konsolidatora > Ogólne > katalogi dodatkowych bibliotek, Dodaj katalog lib\opt hello (np.: C:\Program Files (x86) \MySQL\MySQL C++ łącznika 1.1.9\lib\opt) z hello c ++ Łącznik.
2. W programie Visual Studio wybierz kolejno pozycje Właściwość projektu > Właściwości konfiguracji > C/C++ > Ogólne > Dodatkowe katalogi dyrektywy include
   - Dodaj katalog include/ łącznika języka C++ (tj. C:\Program Files (x86) \MySQL\MySQL Connector C++ 1.1.9\include\)
   - Dodaj katalog główny biblioteki Boost (tj. C:\boost_1_64_0\)
3. W programie Visual Studio projektu właściwości > Właściwości konfiguracji > C/C++ > konsolidatora > wprowadzania > istnieją dodatkowe zależności, Dodaj mysqlcppconn.lib do pola tekstowego hello
4. Albo mysqlcppconn.dll kopiowania z hello c ++ łącznika folder biblioteki w kroku 3 toohello tym samym katalogu co plik wykonywalny aplikacji hello lub dodać toohello zmiennej środowiskowej, można odnaleźć aplikacji.

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **myserver4demo**.
3. Kliknij nazwę serwera hello.
4. Wybierz powitania serwera **właściwości** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.
 ![Nazwa serwera usługi Azure Database for MySQL](./media/connect-cpp/1_server-properties-name-login.png)
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="connect-create-table-and-insert-data"></a>Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych
Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL. Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia. Następnie hello kod używa metody createStatement() i metody execute() toorun hello bazy danych poleceń. 

Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych. 

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

## <a name="read-data"></a>Odczyt danych

Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL. Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia. Następnie hello kod używa metody prepareStatement() i executeQuery() toorun hello wybierz polecenia. Na koniec hello kodzie użyto next() tooadvance toohello rekordów w wynikach hello. Następnie kod hello używa wartości hello tooparse getInt() i getString() w rekordzie hello.

Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych. 

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

## <a name="update-data"></a>Aktualizowanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL. Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia. Następnie hello kod używa metody prepareStatement() i executeQuery() toorun hello polecenia aktualizacji. 

Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych. 

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


## <a name="delete-data"></a>Usuwanie danych
Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **usunąć** instrukcji SQL. Kod Hello używa klasy sql::Driver z tooestablish metody connect() hello tooMySQL połączenia. Następnie hello kod używa metody prepareStatement() i executeQuery() toorun hello Usuń poleceń.

Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych. 

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

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie tooAzure bazy danych programu MySQL bazy danych dla programu MySQL przy użyciu zrzutu i przywracania](concepts-migrate-dump-restore.md)
