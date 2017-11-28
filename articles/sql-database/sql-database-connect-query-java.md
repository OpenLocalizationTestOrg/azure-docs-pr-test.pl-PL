---
title: aaaUse Java tooquery bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "W tym temacie opisano sposób toouse Java toocreate program, który łączy tooan bazy danych SQL Azure i zapytania za pomocą instrukcji języka Transact-SQL."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="75263-103">Użyj Java tooquery bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="75263-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="75263-104">To szybki start pokazano, jak toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooan tooconnect Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="75263-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75263-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="75263-105">Prerequisites</span></span>

<span data-ttu-id="75263-106">toocomplete tym szybki start samouczka, upewnij się, że masz hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="75263-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="75263-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="75263-107">An Azure SQL database.</span></span> <span data-ttu-id="75263-108">To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="75263-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="75263-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="75263-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="75263-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="75263-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="75263-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="75263-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="75263-112">A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.</span><span class="sxs-lookup"><span data-stu-id="75263-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="75263-113">W systemie operacyjnym zainstalowano język Java i związane z nim oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="75263-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="75263-114">**System MacOS**: zainstaluj oprogramowanie Homebrew i Java, a następnie zainstaluj pakiet Maven.</span><span class="sxs-lookup"><span data-stu-id="75263-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="75263-115">Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="75263-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="75263-116">**Ubuntu**: Zainstaluj hello Java Development Kit i zainstaluj Maven.</span><span class="sxs-lookup"><span data-stu-id="75263-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="75263-117">Zobacz [kroki 1.2, 1.3 i 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="75263-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="75263-118">**Windows**: Zainstaluj hello Java Development Kit i Maven.</span><span class="sxs-lookup"><span data-stu-id="75263-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="75263-119">Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="75263-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="75263-120">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="75263-120">SQL server connection information</span></span>

<span data-ttu-id="75263-121">Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="75263-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="75263-122">Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.</span><span class="sxs-lookup"><span data-stu-id="75263-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="75263-123">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75263-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="75263-124">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="75263-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="75263-125">Na powitania **omówienie** bazy danych Przejrzyj, nazwa FQDN serwera hello pokazane na powitania po obrazu: ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.</span><span class="sxs-lookup"><span data-stu-id="75263-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="75263-127">Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="75263-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="75263-128">W razie potrzeby Zresetuj hello hasło.</span><span class="sxs-lookup"><span data-stu-id="75263-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="75263-129">**Utwórz projekt Maven i zależności**</span><span class="sxs-lookup"><span data-stu-id="75263-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="75263-130">Z hello terminali, Utwórz nowy projekt Maven o nazwie **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="75263-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="75263-131">Wprowadź **T** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="75263-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="75263-132">Zmień katalog zbyt**sqltest** , a następnie otwórz ***pom.xml*** o w ulubionym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="75263-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="75263-133">Dodaj hello **sterownik JDBC firmy Microsoft dla programu SQL Server** zależności projektu tooyour przy użyciu hello następujący kod:</span><span class="sxs-lookup"><span data-stu-id="75263-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="75263-134">Również w ***pom.xml***, Dodaj hello następujące właściwości tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="75263-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="75263-135">Jeśli nie masz sekcję właściwości, można dodać go po hello zależności.</span><span class="sxs-lookup"><span data-stu-id="75263-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="75263-136">Zapisz i zamknij plik ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="75263-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="75263-137">Wstaw baza danych SQL tooquery kodu</span><span class="sxs-lookup"><span data-stu-id="75263-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="75263-138">W projekcie Maven w lokalizacji ..\sqltest\src\main\java\com\sqlsamples\App.Java powinien już znajdować się plik o nazwie ***App.java***</span><span class="sxs-lookup"><span data-stu-id="75263-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="75263-139">Otwórz plik hello i zastąp jego zawartość z następujących hello kodu i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="75263-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a><span data-ttu-id="75263-140">Uruchamianie hello kodu</span><span class="sxs-lookup"><span data-stu-id="75263-140">Run hello code</span></span>

1. <span data-ttu-id="75263-141">W wierszu polecenia hello uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="75263-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="75263-142">Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="75263-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="75263-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="75263-143">Next steps</span></span>
- [<span data-ttu-id="75263-144">Projektowanie pierwszej bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="75263-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="75263-145">Sterownik JDBC firmy Microsoft dla programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="75263-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="75263-146">Zgłaszanie problemów/zadawanie pytań</span><span class="sxs-lookup"><span data-stu-id="75263-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

