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
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="90c57-103">Implementowanie wielodostępnych aplikacji SaaS przy użyciu bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="90c57-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="90c57-104">Aplikacja wielodostępne jest aplikacji hostowanej w środowisku chmury i który zawiera ten sam zestaw usług setek lub tysięcy dzierżawców, którzy nie udostępniać lub jego dane są widoczne.</span><span class="sxs-lookup"><span data-stu-id="90c57-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="90c57-105">Przykładem jest aplikacja SaaS, która udostępnia usługi do dzierżawców w środowisku hostowanych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="90c57-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="90c57-106">Ten model izoluje dane dla każdego dzierżawcy i optymalizuje dystrybucji zasobów dla kosztów.</span><span class="sxs-lookup"><span data-stu-id="90c57-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="90c57-107">Ten samouczek przedstawia sposób tworzenia wielodostępnych aplikacji SaaS przy użyciu bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="90c57-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="90c57-108">Z tego samouczka dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="90c57-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="90c57-109">Konfigurowanie środowiska bazy danych do obsługi wielodostępnych aplikacji SaaS, używania wzorca bazy danych na dzierżawy</span><span class="sxs-lookup"><span data-stu-id="90c57-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="90c57-110">Utwórz katalog dzierżawy</span><span class="sxs-lookup"><span data-stu-id="90c57-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="90c57-111">Aprowizację bazy danych dzierżawy i zarejestruj go w katalogu dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="90c57-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="90c57-112">Konfigurowanie przykładowej aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="90c57-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="90c57-113">Dostęp do dzierżawy baz danych prosty aplikację konsoli języka Java</span><span class="sxs-lookup"><span data-stu-id="90c57-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="90c57-114">Usuń dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="90c57-114">Delete a tenant</span></span>

<span data-ttu-id="90c57-115">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="90c57-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90c57-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="90c57-116">Prerequisites</span></span>

<span data-ttu-id="90c57-117">Do ukończenia tego samouczka, upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="90c57-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="90c57-118">Zainstalowana najnowsza wersja środowiska PowerShell i [najnowszy zestaw SDK usługi Azure PowerShell](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="90c57-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="90c57-119">Zainstalowana najnowsza wersja [programu SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="90c57-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="90c57-120">Instalowanie programu SQL Server Management Studio instaluje najnowszą wersję SQLPackage, narzędzie wiersza polecenia, które mogą służyć do automatyzowania szereg zadań związanych z projektowaniem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90c57-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="90c57-121">Zainstalowane [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) i [najnowsze JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) zainstalowana na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="90c57-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="90c57-122">Zainstalowane [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="90c57-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="90c57-123">Maven będzie służyć do zarządzania zależności, tworzenia, testowania i uruchom przykładowy projekt języka Java</span><span class="sxs-lookup"><span data-stu-id="90c57-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="90c57-124">Konfigurowanie środowiska danych</span><span class="sxs-lookup"><span data-stu-id="90c57-124">Set up data environment</span></span>

<span data-ttu-id="90c57-125">Zostanie udostępniania bazy danych dla każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="90c57-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="90c57-126">Model bazy danych dla dzierżawy zapewnia najwyższy stopień izolacji między dzierżawcami małego DevOps kosztów.</span><span class="sxs-lookup"><span data-stu-id="90c57-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="90c57-127">Aby zoptymalizować koszt zasobów w chmurze, zostanie również będą aprowizowane dzierżawy baz danych w puli elastycznej, dzięki czemu można zoptymalizować wydajność ceny dla grupy baz danych.</span><span class="sxs-lookup"><span data-stu-id="90c57-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="90c57-128">Aby dowiedzieć się więcej o innych bazy danych inicjowania obsługi administracyjnej modele [widoczną w tym miejscu](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="90c57-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="90c57-129">Wykonaj następujące kroki, aby utworzyć programu SQL server i puli elastycznej, który będzie obsługiwać wszystkich baz danych dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="90c57-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="90c57-130">Utwórz zmienne do przechowywania wartości, które będą używane w pozostałej części samouczka.</span><span class="sxs-lookup"><span data-stu-id="90c57-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="90c57-131">Upewnij się zmodyfikować zmienną adresu IP na Twój adres IP</span><span class="sxs-lookup"><span data-stu-id="90c57-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
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
   
2. <span data-ttu-id="90c57-132">Logowanie do platformy Azure i utworzenia puli programu SQL server i elastyczna</span><span class="sxs-lookup"><span data-stu-id="90c57-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="90c57-133">Utwórz katalog dzierżawy</span><span class="sxs-lookup"><span data-stu-id="90c57-133">Create tenant catalog</span></span> 

<span data-ttu-id="90c57-134">W wielodostępnych aplikacji SaaS warto wiedzieć, w którym przechowywane są informacje dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="90c57-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="90c57-135">Jest to często przechowywane w bazie katalogu.</span><span class="sxs-lookup"><span data-stu-id="90c57-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="90c57-136">Katalog bazy danych służy do przechowywania mapowania między dzierżawcy i w bazie danych, w którym są przechowywane dane z tej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="90c57-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="90c57-137">Podstawowy wzorzec dotyczy zarówno wielu dzierżawców lub pojedynczej dzierżawy bazy danych jest używany.</span><span class="sxs-lookup"><span data-stu-id="90c57-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="90c57-138">Wykonaj następujące kroki, aby utworzyć bazę danych katalogu dla przykładowej aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="90c57-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="90c57-139">Udostępniania bazy danych dla "tenant1" i zarejestrować się w katalogu dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="90c57-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="90c57-140">Aprowizację bazy danych dla nowej dzierżawy "tenant1" i zarejestrować tej dzierżawy w katalogu przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="90c57-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="90c57-141">Udostępniania bazy danych dla "tenant2" i zarejestrować się w katalogu dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="90c57-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="90c57-142">Aprowizację bazy danych dla nowej dzierżawy "tenant2" i zarejestrować tej dzierżawy w katalogu przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="90c57-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="90c57-143">Konfigurowanie przykładowej aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="90c57-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="90c57-144">Utwórz projekt maven.</span><span class="sxs-lookup"><span data-stu-id="90c57-144">Create a maven project.</span></span> <span data-ttu-id="90c57-145">W oknie wiersza polecenia, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="90c57-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="90c57-146">Dodaj ten zależności, poziom języka i kompilacji opcję obsługi plików manifestu w słoików w pliku pom.xml:</span><span class="sxs-lookup"><span data-stu-id="90c57-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
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

3. <span data-ttu-id="90c57-147">Dodaj następujący kod do pliku App.java:</span><span class="sxs-lookup"><span data-stu-id="90c57-147">Add the following into the App.java file:</span></span>

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

4. <span data-ttu-id="90c57-148">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="90c57-148">Save the file.</span></span>

5. <span data-ttu-id="90c57-149">Przejdź do konsoli poleceń i wykonania</span><span class="sxs-lookup"><span data-stu-id="90c57-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="90c57-150">Po zakończeniu, wykonaj następujące czynności, aby uruchomić aplikację</span><span class="sxs-lookup"><span data-stu-id="90c57-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="90c57-151">Jeśli zostanie wykonane pomyślnie, dane wyjściowe będą następującą postać:</span><span class="sxs-lookup"><span data-stu-id="90c57-151">The output will look like this if it runs successfully:</span></span>

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

## <a name="delete-first-tenant"></a><span data-ttu-id="90c57-152">Usuń pierwszy dzierżawy</span><span class="sxs-lookup"><span data-stu-id="90c57-152">Delete first tenant</span></span> 
<span data-ttu-id="90c57-153">Usuń wpis dzierżawy bazy danych i katalogu dla pierwszego dzierżawcy za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90c57-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

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

<span data-ttu-id="90c57-154">Spróbuj połączyć się "tenant1" przy użyciu aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="90c57-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="90c57-155">Otrzymasz komunikat o błędzie informujący, że dzierżawy nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="90c57-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90c57-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90c57-156">Next steps</span></span> 

<span data-ttu-id="90c57-157">W tym samouczku przedstawiono do:</span><span class="sxs-lookup"><span data-stu-id="90c57-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="90c57-158">Konfigurowanie środowiska bazy danych do obsługi wielodostępnych aplikacji SaaS, używania wzorca bazy danych na dzierżawy</span><span class="sxs-lookup"><span data-stu-id="90c57-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="90c57-159">Utwórz katalog dzierżawy</span><span class="sxs-lookup"><span data-stu-id="90c57-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="90c57-160">Aprowizację bazy danych dzierżawy i zarejestruj go w katalogu dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="90c57-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="90c57-161">Konfigurowanie przykładowej aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="90c57-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="90c57-162">Dostęp do dzierżawy baz danych prosty aplikację konsoli języka Java</span><span class="sxs-lookup"><span data-stu-id="90c57-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="90c57-163">Usuń dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="90c57-163">Delete a tenant</span></span>

* <span data-ttu-id="90c57-164">Przykłady programu PowerShell do wykonywania typowych zadań, zobacz [przykłady środowiska PowerShell bazy danych SQL](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="90c57-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="90c57-165">Projektowanie wzorce dla Zobacz aplikacji SaaS wielodostępne [wzorce projektowe](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="90c57-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="90c57-166">Java przykłady dla typowych zadań Azure, zobacz [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="90c57-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



