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
# <a name="use-java-tooquery-an-azure-sql-database"></a>Użyj Java tooquery bazy danych Azure SQL

To szybki start pokazano, jak toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooan tooconnect Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tym szybki start samouczka, upewnij się, że masz hello następujące wymagania wstępne:

- Baza danych Azure SQL. To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start: 

   - [Tworzenie bazy danych — portal](sql-database-get-started-portal.md)
   - [Tworzenie bazy danych — interfejs wiersza polecenia](sql-database-get-started-cli.md)
   - [Tworzenie bazy danych — PowerShell](sql-database-get-started-powershell.md)

- A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.

- W systemie operacyjnym zainstalowano język Java i związane z nim oprogramowanie.

    - **System MacOS**: zainstaluj oprogramowanie Homebrew i Java, a następnie zainstaluj pakiet Maven. Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: Zainstaluj hello Java Development Kit i zainstaluj Maven. Zobacz [kroki 1.2, 1.3 i 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: Zainstaluj hello Java Development Kit i Maven. Zobacz [kroki 1.2 i 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>Informacje o połączeniu z serwerem SQL

Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database. Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 
3. Na powitania **omówienie** bazy danych Przejrzyj, nazwa FQDN serwera hello pokazane na powitania po obrazu: ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.  

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera.  W razie potrzeby Zresetuj hello hasło.     

## <a name="create-maven-project-and-dependencies"></a>**Utwórz projekt Maven i zależności**
1. Z hello terminali, Utwórz nowy projekt Maven o nazwie **sqltest**. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. Wprowadź **T** po wyświetleniu monitu.
3. Zmień katalog zbyt**sqltest** , a następnie otwórz ***pom.xml*** o w ulubionym edytorze tekstów.  Dodaj hello **sterownik JDBC firmy Microsoft dla programu SQL Server** zależności projektu tooyour przy użyciu hello następujący kod:

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. Również w ***pom.xml***, Dodaj hello następujące właściwości tooyour projektu.  Jeśli nie masz sekcję właściwości, można dodać go po hello zależności.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. Zapisz i zamknij plik ***pom.xml***.

## <a name="insert-code-tooquery-sql-database"></a>Wstaw baza danych SQL tooquery kodu

1. W projekcie Maven w lokalizacji ..\sqltest\src\main\java\com\sqlsamples\App.Java powinien już znajdować się plik o nazwie ***App.java***

2. Otwórz plik hello i zastąp jego zawartość z następujących hello kodu i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.

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

## <a name="run-hello-code"></a>Uruchamianie hello kodu

1. W wierszu polecenia hello uruchom następujące polecenia hello:

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.


## <a name="next-steps"></a>Następne kroki
- [Projektowanie pierwszej bazy danych SQL na platformie Azure](sql-database-design-first-database.md)
- [Sterownik JDBC firmy Microsoft dla programu SQL Server](https://github.com/microsoft/mssql-jdbc)
- [Zgłaszanie problemów/zadawanie pytań](https://github.com/microsoft/mssql-jdbc/issues)

