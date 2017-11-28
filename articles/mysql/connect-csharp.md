---
title: "Połącz tooAzure bazy danych dla programu MySQL w języku C# | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera C# (.NET) kod przykładowy można użyć tooconnect i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="b9a71-103">Bazy danych platformy Azure dla programu MySQL: dane tooconnect i zapytań Użyj .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="b9a71-103">Azure Database for MySQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="b9a71-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="b9a71-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="b9a71-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="b9a71-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="b9a71-106">Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu języka C# oraz czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9a71-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9a71-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9a71-107">Prerequisites</span></span>
<span data-ttu-id="b9a71-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="b9a71-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b9a71-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b9a71-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="b9a71-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b9a71-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="b9a71-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="b9a71-111">You also need to:</span></span>
- <span data-ttu-id="b9a71-112">Zainstalować program [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="b9a71-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="b9a71-113">Wykonaj kroki hello hello połączyć artykuł tooinstall .NET specjalnie dla danej platformy (Windows, Ubuntu Linux lub macOS).</span><span class="sxs-lookup"><span data-stu-id="b9a71-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="b9a71-114">Zainstalować program [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b9a71-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="b9a71-115">Zainstalować [sterownik ODBC dla programu MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="b9a71-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b9a71-116">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="b9a71-116">Get connection information</span></span>
<span data-ttu-id="b9a71-117">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9a71-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="b9a71-118">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="b9a71-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b9a71-119">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9a71-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b9a71-120">Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="b9a71-120">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="b9a71-121">Kliknij nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="b9a71-121">Click hello server name.</span></span>
4. <span data-ttu-id="b9a71-122">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="b9a71-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="b9a71-123">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="b9a71-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b9a71-124">![Nazwa serwera usługi Azure Database for MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b9a71-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b9a71-125">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="b9a71-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b9a71-126">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="b9a71-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="b9a71-127">Użyj hello następujący kod tooconnect i załadować hello danych przy użyciu **CREATE TABLE** i **INSERT INTO** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="b9a71-127">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="b9a71-128">Kod Hello używa klasy ODBC, za pomocą metody [metody Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="b9a71-128">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="b9a71-129">Następnie hello kod używa metody [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), ustawia właściwość CommandText hello i wywołuje metodę [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello bazy danych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b9a71-129">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span> 

<span data-ttu-id="b9a71-130">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b9a71-130">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="b9a71-131">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="b9a71-131">Read data</span></span>

<span data-ttu-id="b9a71-132">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="b9a71-132">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="b9a71-133">Kod Hello używa klasy ODBC, za pomocą metody [metody Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="b9a71-133">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="b9a71-134">Następnie hello kod używa metody [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) i metody [Executereader())](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello bazy danych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b9a71-134">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello database commands.</span></span> <span data-ttu-id="b9a71-135">Następnie hello kod używa [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello rekordów w wynikach hello.</span><span class="sxs-lookup"><span data-stu-id="b9a71-135">Next hello code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="b9a71-136">Następnie kod hello używa wartości hello tooparse GetInt32 i GetString w rekordzie hello.</span><span class="sxs-lookup"><span data-stu-id="b9a71-136">Then hello code uses GetInt32 and GetString tooparse hello values in hello record.</span></span>

<span data-ttu-id="b9a71-137">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b9a71-137">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="b9a71-138">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="b9a71-138">Update data</span></span>
<span data-ttu-id="b9a71-139">Użyj hello następujący kod tooconnect i odczytu hello danych przy użyciu **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="b9a71-139">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="b9a71-140">Kod Hello używa klasy ODBC, za pomocą metody [metody Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="b9a71-140">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="b9a71-141">Następnie hello kod używa metody [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), ustawia właściwość CommandText hello i wywołuje metodę [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello bazy danych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b9a71-141">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="b9a71-142">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b9a71-142">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="b9a71-143">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="b9a71-143">Delete data</span></span>
<span data-ttu-id="b9a71-144">Użyj hello następujący kod tooconnect i usunąć hello danych przy użyciu **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="b9a71-144">Use hello following code tooconnect and delete hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="b9a71-145">Kod Hello używa klasy ODBC, za pomocą metody [metody Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL połączenia.</span><span class="sxs-lookup"><span data-stu-id="b9a71-145">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="b9a71-146">Następnie hello kod używa metody [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), ustawia właściwość CommandText hello i wywołuje metodę [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello bazy danych poleceń.</span><span class="sxs-lookup"><span data-stu-id="b9a71-146">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="b9a71-147">Zastąp parametry hosta, DBName użytkownika i hasło hello wartościami hello określone podczas tworzenia powitania serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b9a71-147">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="b9a71-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b9a71-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b9a71-149">Migrowanie tooAzure bazy danych programu MySQL bazy danych dla programu MySQL przy użyciu zrzutu i przywracania</span><span class="sxs-lookup"><span data-stu-id="b9a71-149">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
