---
title: "Aplikacja SaaS wielodostępne aaaImplement w usłudze Azure SQL Database | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="e5133-103">Implementowanie wielodostępnych aplikacji SaaS przy użyciu bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e5133-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="e5133-104">Aplikacja wielodostępne jest aplikacji hostowanej w środowisku chmury i zapewnia hello sam zestaw usług toohundreds lub tysięcy dzierżawców, którzy nie udostępniać lub jego dane są widoczne.</span><span class="sxs-lookup"><span data-stu-id="e5133-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="e5133-105">Przykładem jest aplikacja SaaS, która zapewnia usługi tootenants w środowisku hostowanych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e5133-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="e5133-106">Ten model izoluje hello danych dla każdego dzierżawcy i optymalizuje dystrybucji hello zasobów dla kosztów.</span><span class="sxs-lookup"><span data-stu-id="e5133-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="e5133-107">W tym samouczku przedstawiono sposób toocreate wielodostępnych aplikacji SaaS przy użyciu bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e5133-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="e5133-108">Z tego samouczka dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="e5133-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e5133-109">Konfigurowanie toosupport środowiska bazy danych wielodostępnych aplikacji SaaS, używania wzorca bazy danych na dzierżawy hello</span><span class="sxs-lookup"><span data-stu-id="e5133-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="e5133-110">Utwórz katalog dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e5133-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="e5133-111">Aprowizację bazy danych dzierżawy i zarejestruj go w katalogu dzierżawcy hello</span><span class="sxs-lookup"><span data-stu-id="e5133-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="e5133-112">Konfigurowanie przykładowej aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="e5133-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="e5133-113">Dostęp do dzierżawy baz danych prosty aplikację konsoli języka Java</span><span class="sxs-lookup"><span data-stu-id="e5133-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="e5133-114">Usuń dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="e5133-114">Delete a tenant</span></span>

<span data-ttu-id="e5133-115">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="e5133-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5133-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e5133-116">Prerequisites</span></span>

<span data-ttu-id="e5133-117">toocomplete tego samouczka, upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="e5133-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="e5133-118">Hello zainstalowana najnowsza wersja programu PowerShell i hello [najnowszy zestaw SDK usługi Azure PowerShell](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e5133-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="e5133-119">Hello zainstalowana najnowsza wersja [programu SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="e5133-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="e5133-120">Instalowanie programu SQL Server Management Studio instaluje najnowszą wersję hello SQLPackage, narzędzie wiersza polecenia, które mogą być używane tooautomate szereg zadań związanych z projektowaniem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e5133-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="e5133-121">Zainstalowane hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) i hello [najnowsze JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) zainstalowana na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e5133-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="e5133-122">Zainstalowane [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="e5133-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="e5133-123">Maven będą używane toohelp Zarządzanie zależności, tworzenia, testowania i uruchom hello przykładowy projekt języka Java</span><span class="sxs-lookup"><span data-stu-id="e5133-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="e5133-124">Konfigurowanie środowiska danych</span><span class="sxs-lookup"><span data-stu-id="e5133-124">Set up data environment</span></span>

<span data-ttu-id="e5133-125">Zostanie udostępniania bazy danych dla każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="e5133-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="e5133-126">model bazy danych dla dzierżawy Hello zapewnia najwyższy stopień izolacji między dzierżawcami małego kosztów DevOps hello.</span><span class="sxs-lookup"><span data-stu-id="e5133-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="e5133-127">Koszt hello toooptimize zasobów w chmurze, zostanie również będą aprowizowane hello dzierżawcy z bazy danych w puli elastycznej, dzięki czemu można toooptimize hello ceny wydajności dla grupy baz danych.</span><span class="sxs-lookup"><span data-stu-id="e5133-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="e5133-128">toolearn o drugiej bazie danych inicjowania obsługi administracyjnej modele [widoczną w tym miejscu](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="e5133-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="e5133-129">Wykonaj te kroki toocreate programu SQL server i puli elastycznej, który będzie obsługiwać wszystkich baz danych dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e5133-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="e5133-130">Utwórz zmienne toostore wartości, które będą używane w rest hello hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="e5133-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="e5133-131">Upewnij się, że toomodify hello IP adresu zmiennej tooinclude adresu IP</span><span class="sxs-lookup"><span data-stu-id="e5133-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="e5133-132">TooAzure logowania i utworzenia puli programu SQL server i elastyczna</span><span class="sxs-lookup"><span data-stu-id="e5133-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="e5133-133">Utwórz katalog dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e5133-133">Create tenant catalog</span></span> 

<span data-ttu-id="e5133-134">W wielodostępnych aplikacji SaaS jest ważne tooknow, w którym przechowywane są informacje dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e5133-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="e5133-135">Jest to często przechowywane w bazie katalogu.</span><span class="sxs-lookup"><span data-stu-id="e5133-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="e5133-136">Baza danych katalogu Hello jest używany toohold mapowanie między dzierżawcy i w bazie danych, w którym są przechowywane dane z tej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e5133-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="e5133-137">podstawowy wzorzec Hello dotyczy zarówno wielu dzierżawców lub pojedynczej dzierżawy bazy danych jest używany.</span><span class="sxs-lookup"><span data-stu-id="e5133-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="e5133-138">Wykonaj te kroki toocreate bazy danych katalogu hello przykładowej aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e5133-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="e5133-139">Udostępniania bazy danych dla "tenant1" i zarejestrować się w katalogu dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="e5133-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="e5133-140">Użyj programu Powershell tooprovision bazy danych dla nowej dzierżawy "tenant1" i zarejestruj tej dzierżawy w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e5133-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register 'tenant1' in hello tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="e5133-141">Udostępniania bazy danych dla "tenant2" i zarejestrować się w katalogu dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="e5133-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="e5133-142">Użyj programu Powershell tooprovision bazy danych dla nowej dzierżawy "tenant2" i zarejestruj tej dzierżawy w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e5133-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register tenant 'tenant2' in hello tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="e5133-143">Konfigurowanie przykładowej aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="e5133-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="e5133-144">Utwórz projekt maven.</span><span class="sxs-lookup"><span data-stu-id="e5133-144">Create a maven project.</span></span> <span data-ttu-id="e5133-145">W oknie wiersza polecenia, wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e5133-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="e5133-146">Dodaj ten zależności, poziom języka i kompilacja toosupport opcji manifestu plików w pliku pom.xml toohello słoików:</span><span class="sxs-lookup"><span data-stu-id="e5133-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="e5133-147">Dodaj następujące hello do pliku App.java hello:</span><span class="sxs-lookup"><span data-stu-id="e5133-147">Add hello following into hello App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
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
   
   // List all tenants that currently exist in hello system
   
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
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
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

4. <span data-ttu-id="e5133-148">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="e5133-148">Save hello file.</span></span>

5. <span data-ttu-id="e5133-149">Przejdź do konsoli toocommand i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="e5133-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="e5133-150">Po zakończeniu wykonywania powitania po aplikacji hello toorun</span><span class="sxs-lookup"><span data-stu-id="e5133-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="e5133-151">Witaj danych wyjściowych będzie wyglądać następująco Jeśli zostanie wykonane pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="e5133-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="e5133-152">Usuń pierwszy dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e5133-152">Delete first tenant</span></span> 
<span data-ttu-id="e5133-153">Dla dzierżawcy pierwszy hello, należy użyć programu PowerShell toodelete hello dzierżawy bazy danych i wykaz wpisu.</span><span class="sxs-lookup"><span data-stu-id="e5133-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="e5133-154">Spróbuj nawiązać połączenie za pomocą "tenant1" hello aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="e5133-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="e5133-155">Otrzymasz komunikat o błędzie informujący, że dzierżawy hello nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="e5133-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5133-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5133-156">Next steps</span></span> 

<span data-ttu-id="e5133-157">W tym samouczku przedstawiono do:</span><span class="sxs-lookup"><span data-stu-id="e5133-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e5133-158">Konfigurowanie toosupport środowiska bazy danych wielodostępnych aplikacji SaaS, używania wzorca bazy danych na dzierżawy hello</span><span class="sxs-lookup"><span data-stu-id="e5133-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="e5133-159">Utwórz katalog dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e5133-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="e5133-160">Aprowizację bazy danych dzierżawy i zarejestruj go w katalogu dzierżawcy hello</span><span class="sxs-lookup"><span data-stu-id="e5133-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="e5133-161">Konfigurowanie przykładowej aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="e5133-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="e5133-162">Dostęp do dzierżawy baz danych prosty aplikację konsoli języka Java</span><span class="sxs-lookup"><span data-stu-id="e5133-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="e5133-163">Usuń dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="e5133-163">Delete a tenant</span></span>

* <span data-ttu-id="e5133-164">Przykłady programu PowerShell do wykonywania typowych zadań, zobacz [przykłady środowiska PowerShell bazy danych SQL](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="e5133-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="e5133-165">Projektowanie wzorce dla Zobacz aplikacji SaaS wielodostępne [wzorce projektowe](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="e5133-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="e5133-166">Java przykłady dla typowych zadań Azure, zobacz [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="e5133-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



