---
title: "Implementowanie wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Implementuje wielodostępnych aplikacji SaaS z bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Implementowanie wielodostępnych aplikacji SaaS przy użyciu bazy danych SQL Azure

Aplikacja wielodostępne jest aplikacji hostowanej w środowisku chmury i który zawiera ten sam zestaw usług setek lub tysięcy dzierżawców, którzy nie udostępniać lub jego dane są widoczne. Przykładem jest aplikacja SaaS, która udostępnia usługi do dzierżawców w środowisku hostowanych w chmurze. Ten model izoluje dane dla każdego dzierżawcy i optymalizuje dystrybucji zasobów dla kosztów. 

Ten samouczek przedstawia sposób tworzenia wielodostępnych aplikacji SaaS przy użyciu bazy danych SQL Azure.

Z tego samouczka dowiesz się:
> [!div class="checklist"]
> * Konfigurowanie środowiska bazy danych do obsługi wielodostępnych aplikacji SaaS, używania wzorca bazy danych na dzierżawy
> * Utwórz katalog dzierżawy
> * Aprowizację bazy danych dzierżawy i zarejestruj go w katalogu dzierżawcy
> * Konfigurowanie przykładowej aplikacji Java 
> * Dostęp do dzierżawy baz danych prosty aplikację konsoli języka Java
> * Usuń dzierżawcy

Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.

## <a name="prerequisites"></a>Wymagania wstępne

Do ukończenia tego samouczka, upewnij się, że masz:

* Zainstalowana najnowsza wersja środowiska PowerShell i [najnowszy zestaw SDK usługi Azure PowerShell](http://azure.microsoft.com/downloads/)

* Zainstalowana najnowsza wersja [programu SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Instalowanie programu SQL Server Management Studio instaluje najnowszą wersję SQLPackage, narzędzie wiersza polecenia, które mogą służyć do automatyzowania szereg zadań związanych z projektowaniem bazy danych.

* Zainstalowane [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) i [najnowsze JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) zainstalowana na tym komputerze. 

* Zainstalowane [Apache Maven](https://maven.apache.org/download.cgi). Maven będzie służyć do zarządzania zależności, tworzenia, testowania i uruchom przykładowy projekt języka Java

## <a name="set-up-data-environment"></a>Konfigurowanie środowiska danych

Zostanie udostępniania bazy danych dla każdego dzierżawcy. Model bazy danych dla dzierżawy zapewnia najwyższy stopień izolacji między dzierżawcami małego DevOps kosztów. Aby zoptymalizować koszt zasobów w chmurze, zostanie również będą aprowizowane dzierżawy baz danych w puli elastycznej, dzięki czemu można zoptymalizować wydajność ceny dla grupy baz danych. Aby dowiedzieć się więcej o innych bazy danych inicjowania obsługi administracyjnej modele [widoczną w tym miejscu](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Wykonaj następujące kroki, aby utworzyć programu SQL server i puli elastycznej, który będzie obsługiwać wszystkich baz danych dzierżawy. 

1. Utwórz zmienne do przechowywania wartości, które będą używane w pozostałej części samouczka. Upewnij się zmodyfikować zmienną adresu IP na Twój adres IP 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. Logowanie do platformy Azure i utworzenia puli programu SQL server i elastyczna 
   
   ```PowerShell
   # Login to Azure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a>Utwórz katalog dzierżawy 

W wielodostępnych aplikacji SaaS warto wiedzieć, w którym przechowywane są informacje dla dzierżawy. Jest to często przechowywane w bazie katalogu. Katalog bazy danych służy do przechowywania mapowania między dzierżawcy i w bazie danych, w którym są przechowywane dane z tej dzierżawy.  Podstawowy wzorzec dotyczy zarówno wielu dzierżawców lub pojedynczej dzierżawy bazy danych jest używany.

Wykonaj następujące kroki, aby utworzyć bazę danych katalogu dla przykładowej aplikacji SaaS.

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Udostępniania bazy danych dla "tenant1" i zarejestrować się w katalogu dzierżawcy 
Aprowizację bazy danych dla nowej dzierżawy "tenant1" i zarejestrować tej dzierżawy w katalogu przy użyciu programu Powershell. 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Udostępniania bazy danych dla "tenant2" i zarejestrować się w katalogu dzierżawcy
Aprowizację bazy danych dla nowej dzierżawy "tenant2" i zarejestrować tej dzierżawy w katalogu przy użyciu programu Powershell. 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a>Konfigurowanie przykładowej aplikacji Java 

1. Utwórz projekt maven. W oknie wiersza polecenia, wpisz następujące polecenie:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Dodaj ten zależności, poziom języka i kompilacji opcję obsługi plików manifestu w słoików w pliku pom.xml:
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. Dodaj następujący kod do pliku App.java:

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in the system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. Zapisz plik.

5. Przejdź do konsoli poleceń i wykonania

   ```bash
   mvn package
   ```

6. Po zakończeniu, wykonaj następujące czynności, aby uruchomić aplikację 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
Jeśli zostanie wykonane pomyślnie, dane wyjściowe będą następującą postać:

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a>Usuń pierwszy dzierżawy 
Usuń wpis dzierżawy bazy danych i katalogu dla pierwszego dzierżawcy za pomocą programu PowerShell.

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

Spróbuj połączyć się "tenant1" przy użyciu aplikacji Java. Otrzymasz komunikat o błędzie informujący, że dzierżawy nie istnieje.

## <a name="next-steps"></a>Następne kroki 

W tym samouczku przedstawiono do:
> [!div class="checklist"]
> * Konfigurowanie środowiska bazy danych do obsługi wielodostępnych aplikacji SaaS, używania wzorca bazy danych na dzierżawy
> * Utwórz katalog dzierżawy
> * Aprowizację bazy danych dzierżawy i zarejestruj go w katalogu dzierżawcy
> * Konfigurowanie przykładowej aplikacji Java 
> * Dostęp do dzierżawy baz danych prosty aplikację konsoli języka Java
> * Usuń dzierżawcy

* Przykłady programu PowerShell do wykonywania typowych zadań, zobacz [przykłady środowiska PowerShell bazy danych SQL](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Projektowanie wzorce dla Zobacz aplikacji SaaS wielodostępne [wzorce projektowe](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Java przykłady dla typowych zadań Azure, zobacz [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/)



