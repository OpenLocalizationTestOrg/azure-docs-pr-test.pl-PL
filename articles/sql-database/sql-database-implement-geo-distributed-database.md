---
title: "aaaImplement rozwiązania bazy danych SQL Azure rozproszona geograficznie | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooconfigure bazy danych SQL Azure i aplikacji dla trybu failover tooa replikowane bazy danych i testowanie trybu failover."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a>Wdrożenie rozproszone geograficznie bazy danych

W tym samouczku skonfiguruj bazy danych Azure SQL i aplikacji dla trybu failover tooa zdalnego regionu, a następnie testować tryb failover planu. Omawiane kwestie: 

> [!div class="checklist"]
> * Tworzenie bazy danych użytkowników i udzielić im uprawnień
> * Skonfiguruj regułę zapory poziomu bazy danych
> * Utwórz [— replikacja geograficzna trybu failover grupy](sql-database-geo-replication-overview.md)
> * Tworzenie i kompilacja tooquery aplikacji Java bazy danych Azure SQL
> * Wykonaj wyszczególniania odzyskiwania po awarii

Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.


## <a name="prerequisites"></a>Wymagania wstępne

toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

- Najnowsza wersja zainstalowanego hello [programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Zainstalowana baza danych Azure SQL. W tym samouczku używana hello AdventureWorksLT przykładowa baza danych o nazwie **mySampleDatabase** z jednego z tych Szybki Start:

   - [Tworzenie bazy danych — portal](sql-database-get-started-portal.md)
   - [Tworzenie bazy danych — interfejs wiersza polecenia](sql-database-get-started-cli.md)
   - [Tworzenie bazy danych — PowerShell](sql-database-get-started-powershell.md)

- Zidentyfikowano tooexecute metody SQL skryptów bazy danych, można użyć jednej z hello następujące narzędzia kwerendy:
   - Edytor zapytań Hello w hello [portalu Azure](https://portal.azure.com). Aby uzyskać więcej informacji na temat używania edytora zapytań hello w hello portalu Azure, zobacz [Connect i zapytania za pomocą edytora zapytań](sql-database-get-started-portal.md#query-the-sql-database).
   - Witaj najnowsza wersja [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), która jest zintegrowane środowisko umożliwiające zarządzanie dowolnej infrastruktury SQL z programu SQL Server tooSQL bazy danych systemu Microsoft Windows.
   - Hello najnowsza wersja [Visual Studio Code](https://code.visualstudio.com/docs), czyli edytorze graficznego kodu dla systemu Linux, macOS, i systemu Windows, które obsługuje rozszerzenia, w tym hello [rozszerzenia mssql](https://aka.ms/mssql-marketplace) do wykonywania zapytań programu Microsoft SQL Server , Baza danych azure SQL i SQL Data Warehouse. Aby uzyskać więcej informacji o usłudze Azure SQL Database za pomocą tego narzędzia, zobacz [Connect i zapytanie z kodem VS](sql-database-connect-query-vscode.md). 

## <a name="create-database-users-and-grant-permissions"></a>Tworzenie bazy danych użytkowników i udzielanie uprawnień

Łączenie tooyour bazy danych i tworzenie kont użytkowników przy użyciu jednej z hello następujące narzędzia kwerendy:

- Edytor zapytań Hello w hello portalu Azure
- SQL Server Management Studio
- Visual Studio Code

Te konta użytkowników automatycznie replikowane tooyour pomocniczy serwer (i są synchronizowane). toouse SQL Server Management Studio lub Visual Studio Code, jeśli nawiązujesz połączenie z klienta na adres IP, dla którego nie została jeszcze skonfigurowana zapora może być konieczne tooconfigure reguły zapory. Aby uzyskać szczegółowe instrukcje, zobacz [utworzyć regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).

- W oknie zapytania należy wykonać hello następującego zapytania toocreate dwóch kont użytkownika w bazie danych. Ten skrypt przyznaje **db_owner** toohello uprawnienia **app_admin** konto i przyznaje **wybierz** i **aktualizacji** toohello uprawnień **app_user** konta. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Utwórz zapory poziomu bazy danych

Utwórz [reguły zapory poziomu bazy danych](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) bazy danych SQL. Ta reguła zapory poziomu bazy danych automatycznie replikuje toohello serwera pomocniczego, utworzone w tym samouczku. Dla uproszczenia (w tym samouczku) Użyj publicznego adresu IP hello hello komputera, na którym hello kroki są wykonywane w ramach tego samouczka. adres IP hello toodetermine używany dla reguły zapory poziomu serwera hello na tym samym komputerze, zobacz [utworzenie zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- W oknie zapytania otwarte należy zastąpić poprzednie zapytanie hello hello następującego zapytania, zastępując adresy IP hello hello odpowiednie adresy IP dla danego środowiska.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Utwórz grupę aktywna replikacja geograficzna automatycznej pracy awaryjnej 

Przy użyciu programu Azure PowerShell utworzyć [aktywna replikacja geograficzna automatycznej pracy awaryjnej grupy](sql-database-geo-replication-overview.md) między istniejącego serwera Azure SQL i hello nowy pusty serwera Azure SQL w regionie Azure, a następnie dodaj grupy pracy awaryjnej toohello przykładowej bazy danych.

> [!IMPORTANT]
> Te polecenia cmdlet wymagają programu Azure PowerShell 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Wypełnić zmienne dla skryptów PowerShell przy użyciu wartości hello istniejącego serwera i przykładową bazę danych i podaj globalnie unikatowa wartość nazwy grupy pracy awaryjnej.

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. W danym regionie trybu failover, należy utworzyć pusty serwer kopii zapasowej.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Utwórz grupę trybu failover między dwoma serwerami hello.

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. Dodaj grupy pracy awaryjnej toohello bazy danych.

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a>Instalowanie oprogramowania Java

kroki Hello w tej sekcji założono, że znasz tworzenie przy użyciu języka Java i są nowe tooworking z bazy danych SQL Azure. 

### <a name="mac-os"></a>**Mac OS**
Otwórz terminala i przejdź do katalogu tooa, w którym planujesz utworzenie projektu języka Java. Zainstaluj **brew** i **Maven** wprowadzając hello następującego polecenia: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź hello [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję **MacOS**i postępuj Witaj szczegółowe instrukcje dotyczące konfigurowania Java i Maven w kroku 1.2 i 1.3.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Otwórz terminala i przejdź do katalogu tooa, w którym planujesz utworzenie projektu języka Java. Zainstaluj **Maven** wprowadzając hello następującego polecenia:

```bash
sudo apt-get install maven
```

Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź hello [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję **Ubuntu**i postępuj Witaj szczegółowe instrukcje dotyczące konfigurowania Java i Maven w kroku 1.2, 1.3 i 1.4.

### <a name="windows"></a>**Windows**
Zainstaluj [Maven](https://maven.apache.org/download.cgi) za pomocą Instalatora oficjalnego hello. Używanie programu Maven toohelp Zarządzanie zależności, tworzenia, testowania i uruchom projekt języka Java. Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź hello [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję Windows, a następnie wykonaj hello szczegółowe instrukcje dotyczące Konfigurowanie języka Java i Maven w kroku 1.2 i 1.3.

## <a name="create-sqldbsample-project"></a>Utwórz projekt SqlDbSample

1. W konsoli polecenie hello (na przykład Bash) Utwórz projekt Maven. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Typ **Y** i kliknij przycisk **Enter**.
3. Przejdź do nowo utworzonego projektu.

   ```bash
   cd SqlDbSamples
   ```

4. Za pomocą ulubionego edytora, otwórz plik pom.xml hello w folderze projektu. 

5. Dodaj hello sterownik JDBC firmy Microsoft dla programu SQL Server zależności tooyour Maven project przez otwarcie w ulubionym edytorze tekstów i kopiowanie i wklejanie hello następujące wiersze do pliku pom.xml. Nie zastępuj istniejące wartości hello wypełniony hello pliku. Hello zależności JDBC należy wkleić w ciągu (hello większych "zależności" sekcji).   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Określ wersję hello Java toocompile hello projektu w odniesieniu do przez dodanie powitania po sekcji "właściwości" w pliku pom.xml powitania po sekcji "zależności" hello. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Dodaj następujące hello "kompilacji" sekcji w pliku pom.xml powitania po hello "właściwości" sekcji toosupport pliki manifestu w słoików.       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. Zapisz i zamknij plik pom.xml hello.
9. Otwórz plik App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) i Zastąp zawartość hello powitania po zawartości. Zastąp nazwę grupy pracy awaryjnej hello hello nazwę grupy pracy awaryjnej. Zmiana wartości hello hello Nazwa bazy danych użytkownika lub hasło, należy zmienić także te wartości.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. Zapisz i zamknij plik App.java hello.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Kompilowanie i uruchamianie projektu SqlDbSample hello

1. W konsoli poleceń hello wykonaj polecenie toofollowing.

   ```bash
   mvn package
   ```
2. Po zakończeniu wykonywania powitania po aplikacji hello toorun poleceń (działa na godzinę, chyba że zostanie zatrzymana ręcznie):

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Wykonaj wyszczególniania odzyskiwania po awarii

1. Wywołanie ręcznego przełączania trybu failover grupy pracy awaryjnej. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Obserwować wyniki aplikacji hello, podczas pracy awaryjnej. Niektóre wstawia się niepowodzeniem podczas odświeżania pamięci podręcznej DNS hello.     

3. Dowiedz się od roli działa serwer odzyskiwania po awarii.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Powrót po awarii.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Należy obserwować wyniki aplikacji hello podczas powrotu po awarii. Niektóre wstawia się niepowodzeniem podczas odświeżania pamięci podręcznej DNS hello.     

6. Dowiedz się od roli działa serwer odzyskiwania po awarii.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Następne kroki 

Aby uzyskać więcej informacji, zobacz [aktywnych grup — replikacja geograficzna i pracy awaryjnej](sql-database-geo-replication-overview.md).
