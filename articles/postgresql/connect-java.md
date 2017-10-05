---
title: "Nawiązywanie połączeń z usługą Azure Database for PostgreSQL za pomocą języka Java | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera przykładowy kod Java, którego można używać do nawiązywania połączeń z danymi usługi Azure Database for PostgreSQL i wykonywania zapytań względem nich."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="3d323-103">Usługa Azure Database for PostgreSQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań za pomocą języka Java</span><span class="sxs-lookup"><span data-stu-id="3d323-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="3d323-104">Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for PostgreSQL przy użyciu aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="3d323-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="3d323-105">Pokazano w nim, jak używać instrukcji języka SQL w celu wysyłania zapytań o dane oraz wstawiania, aktualizowania i usuwania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="3d323-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="3d323-106">W krokach w tym artykule założono, że wiesz już, jak programować za pomocą języka Java, i dopiero zaczynasz pracę z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3d323-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d323-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3d323-107">Prerequisites</span></span>
<span data-ttu-id="3d323-108">Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:</span><span class="sxs-lookup"><span data-stu-id="3d323-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3d323-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="3d323-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="3d323-110">Tworzenie bazy danych — interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3d323-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="3d323-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="3d323-111">You also need to:</span></span>
- <span data-ttu-id="3d323-112">Pobrać [sterownik JDBC programu PostgreSQL](https://jdbc.postgresql.org/download.html) zgodny z używaną wersją języka Java i zestawu Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="3d323-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="3d323-113">Uwzględnić plik jar JDBC programu PostgreSQL (na przykład postgresql-42.1.1.jar) w ścieżce klasy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d323-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="3d323-114">Aby uzyskać więcej informacji, zobacz [szczegóły ścieżki klasy](https://jdbc.postgresql.org/documentation/head/classpath.html).</span><span class="sxs-lookup"><span data-stu-id="3d323-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3d323-115">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="3d323-115">Get connection information</span></span>
<span data-ttu-id="3d323-116">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z usługą Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3d323-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="3d323-117">Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="3d323-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3d323-118">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3d323-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3d323-119">W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="3d323-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="3d323-120">Kliknij nazwę serwera **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="3d323-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="3d323-121">Wybierz stronę serwera **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="3d323-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="3d323-122">Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="3d323-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3d323-123">![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="3d323-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="3d323-124">Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="3d323-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="3d323-125">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="3d323-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="3d323-126">Użyj poniższego kodu, aby nawiązać połączenie i załadować dane przy użyciu funkcji z instrukcją **INSERT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="3d323-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="3d323-127">Metody [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) i [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) są używane do nawiązywania połączenia, usuwania i tworzenia tabeli.</span><span class="sxs-lookup"><span data-stu-id="3d323-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="3d323-128">Obiekt [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) jest używany do tworzenia poleceń insert, z metodami setString() i setInt() do powiązania wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="3d323-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="3d323-129">Metoda [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) uruchamia polecenie dla każdego zestawu parametrów.</span><span class="sxs-lookup"><span data-stu-id="3d323-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="3d323-130">Zastąp parametry hosta, bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia własnego serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3d323-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="3d323-131">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="3d323-131">Read data</span></span>
<span data-ttu-id="3d323-132">Użyj poniższego kodu, aby odczytać dane za pomocą instrukcji **SELECT** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="3d323-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="3d323-133">Metody [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) i [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) są używane do nawiązywania połączenia, tworzenia i uruchamiania instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="3d323-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="3d323-134">Wyniki są przetwarzane przy użyciu obiektu [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html).</span><span class="sxs-lookup"><span data-stu-id="3d323-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="3d323-135">Zastąp parametry hosta, bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia własnego serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3d323-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="3d323-136">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="3d323-136">Update data</span></span>
<span data-ttu-id="3d323-137">Użyj poniższego kodu, aby zmienić dane za pomocą instrukcji **UPDATE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="3d323-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="3d323-138">Metody [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) i [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) są używane do nawiązywania połączenia, przygotowywania i uruchamiania instrukcji UPDATE.</span><span class="sxs-lookup"><span data-stu-id="3d323-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="3d323-139">Zastąp parametry hosta, bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia własnego serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3d323-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="3d323-140">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="3d323-140">Delete data</span></span>
<span data-ttu-id="3d323-141">Użyj poniższego kodu, aby usunąć dane za pomocą instrukcji **DELETE** języka SQL.</span><span class="sxs-lookup"><span data-stu-id="3d323-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="3d323-142">Metody [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) i [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) są używane do nawiązywania połączenia, przygotowywania i uruchamiania instrukcji DELETE.</span><span class="sxs-lookup"><span data-stu-id="3d323-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="3d323-143">Zastąp parametry hosta, bazy danych, użytkownika i hasła wartościami, które zostały określone podczas tworzenia własnego serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3d323-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3d323-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d323-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3d323-145">Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="3d323-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
