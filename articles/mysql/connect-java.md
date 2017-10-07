---
title: "Połącz tooAzure bazy danych dla programu MySQL przy użyciu języka Java | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera przykładowy kod języka Java można użyć tooconnect i zapytania na danych z bazy danych Azure dla bazy danych MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="5f927-103">Bazy danych platformy Azure dla programu MySQL: Użyj języka Java tooconnect i zapytań danych.</span><span class="sxs-lookup"><span data-stu-id="5f927-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="5f927-104">Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL przy użyciu aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="5f927-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="5f927-105">Widoczny jest sposób toouse tooquery instrukcji SQL, wstawiania, aktualizowania i usuwania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5f927-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="5f927-106">Hello krokach w tym artykule przyjęto założenie, że znasz tworzenie przy użyciu języka Java i czy są nowe tooworking z bazą danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f927-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f927-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5f927-107">Prerequisites</span></span>
<span data-ttu-id="5f927-108">Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:</span><span class="sxs-lookup"><span data-stu-id="5f927-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5f927-109">Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f927-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="5f927-110">Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5f927-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="5f927-111">Należy również:</span><span class="sxs-lookup"><span data-stu-id="5f927-111">You also need to:</span></span>
- <span data-ttu-id="5f927-112">Pobierz sterownik JDBC hello [MySQL łącznika/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="5f927-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="5f927-113">Uwzględnij plik jar JDBC hello (na przykład mysql — łącznik java-5.1.42-bin.jar) w ścieżce klas aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5f927-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="5f927-114">Jeśli masz z tym problem, zapoznaj się z charakterystyką ścieżki klas w dokumentacji dotyczącej środowisk, takich jak [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) lub [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="5f927-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="5f927-115">Upewnij się, że bazy danych Azure, zabezpieczenia połączeń MySQL skonfigurowano zapory hello otwarty i ustawienia protokołu SSL dostosowana do Twojej aplikacji tooconnect pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5f927-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5f927-116">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="5f927-116">Get connection information</span></span>
<span data-ttu-id="5f927-117">Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f927-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="5f927-118">Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="5f927-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5f927-119">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5f927-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5f927-120">W okienku po lewej stronie powitania kliknij **wszystkie zasoby**, a następnie wyszukaj serwera hello utworzono (na przykład **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="5f927-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="5f927-121">Kliknij nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="5f927-121">Click hello server name.</span></span>
4. <span data-ttu-id="5f927-122">Wybierz powitania serwera **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="5f927-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="5f927-123">Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="5f927-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5f927-124">![Nazwa serwera usługi Azure Database for MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5f927-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5f927-125">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="5f927-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5f927-126">Nawiązywanie połączenia, tworzenie tabeli i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="5f927-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="5f927-127">Witaj Użyj następującego kodu tooconnect i obciążenia hello danych przy użyciu funkcji hello z **Wstaw** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5f927-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="5f927-128">Witaj [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) tooMySQL tooconnect używana jest metoda.</span><span class="sxs-lookup"><span data-stu-id="5f927-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="5f927-129">Metody [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) i metody execute() są używane toodrop i utworzyć hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="5f927-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="5f927-130">Obiekt prepareStatement Hello jest toobuild używanych poleceń insert hello, z wartościami parametru hello toobind setString() i setInt().</span><span class="sxs-lookup"><span data-stu-id="5f927-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="5f927-131">Metoda executeUpdate() uruchamia polecenie powitania dla każdego zestawu parametrów tooinsert hello wartości.</span><span class="sxs-lookup"><span data-stu-id="5f927-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="5f927-132">Zamień hello hosta, bazy danych użytkownika i hasło Parametry hello wartości, które określono podczas tworzenia własnych serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5f927-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="read-data"></a><span data-ttu-id="5f927-133">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="5f927-133">Read data</span></span>
<span data-ttu-id="5f927-134">Użyj hello poniższy kod tooread hello danych za pomocą **wybierz** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5f927-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="5f927-135">Witaj [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) tooMySQL tooconnect używana jest metoda.</span><span class="sxs-lookup"><span data-stu-id="5f927-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="5f927-136">Witaj metody [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) i executeQuery() są używane tooconnect i uruchom hello instrukcji select.</span><span class="sxs-lookup"><span data-stu-id="5f927-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="5f927-137">wyniki Hello są przetwarzane przy użyciu [zestaw wyników](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) obiektu.</span><span class="sxs-lookup"><span data-stu-id="5f927-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="5f927-138">Zamień hello hosta, bazy danych użytkownika i hasło Parametry hello wartości, które określono podczas tworzenia własnych serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5f927-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="5f927-139">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="5f927-139">Update data</span></span>
<span data-ttu-id="5f927-140">Użyj hello poniższy kod toochange hello danych za pomocą **aktualizacji** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5f927-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="5f927-141">Witaj [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) tooMySQL tooconnect używana jest metoda.</span><span class="sxs-lookup"><span data-stu-id="5f927-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="5f927-142">Witaj metody [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) i executeUpdate() są używane tooprepare i uruchom hello instrukcji update.</span><span class="sxs-lookup"><span data-stu-id="5f927-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="5f927-143">Zamień hello hosta, bazy danych użytkownika i hasło Parametry hello wartości, które określono podczas tworzenia własnych serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5f927-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="5f927-144">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="5f927-144">Delete data</span></span>
<span data-ttu-id="5f927-145">Użyj hello poniższy kod tooremove danych za pomocą **usunąć** instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="5f927-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="5f927-146">Witaj [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) tooMySQL tooconnect używana jest metoda.</span><span class="sxs-lookup"><span data-stu-id="5f927-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="5f927-147">Witaj metody [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) i executeUpdate() są używane tooprepare i uruchom hello instrukcji update.</span><span class="sxs-lookup"><span data-stu-id="5f927-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="5f927-148">Zamień hello hosta, bazy danych użytkownika i hasło Parametry hello wartości, które określono podczas tworzenia własnych serwera i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5f927-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5f927-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f927-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5f927-150">Migrowanie tooAzure bazy danych programu MySQL bazy danych dla programu MySQL przy użyciu zrzutu i przywracania</span><span class="sxs-lookup"><span data-stu-id="5f927-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
