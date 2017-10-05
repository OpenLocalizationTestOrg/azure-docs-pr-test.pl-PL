---
title: "Wdrożenia rozwiązania bazy danych SQL Azure rozproszona geograficznie | Dokumentacja firmy Microsoft"
description: "Dowiedz się do konfigurowania bazy danych SQL Azure i aplikacji dla trybu failover z bazą danych replikowanych i testowanie trybu failover."
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
ms.openlocfilehash: 9f53f318e20dac9248906bdbe898ba4dacb286ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="22e1d-103">Wdrożenie rozproszone geograficznie bazy danych</span><span class="sxs-lookup"><span data-stu-id="22e1d-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="22e1d-104">W tym samouczku skonfiguruj bazy danych Azure SQL i aplikacji dla trybu failover w regionie zdalnego, a następnie testować tryb failover planu.</span><span class="sxs-lookup"><span data-stu-id="22e1d-104">In this tutorial, you configure an Azure SQL database and application for failover to a remote region, and then test your failover plan.</span></span> <span data-ttu-id="22e1d-105">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="22e1d-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="22e1d-106">Tworzenie bazy danych użytkowników i udzielić im uprawnień</span><span class="sxs-lookup"><span data-stu-id="22e1d-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="22e1d-107">Skonfiguruj regułę zapory poziomu bazy danych</span><span class="sxs-lookup"><span data-stu-id="22e1d-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="22e1d-108">Utwórz [— replikacja geograficzna trybu failover grupy](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="22e1d-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="22e1d-109">Tworzenie i kompilacja aplikacji Java kwerendy bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="22e1d-109">Create and compile a Java application to query an Azure SQL database</span></span>
> * <span data-ttu-id="22e1d-110">Wykonaj wyszczególniania odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="22e1d-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="22e1d-111">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="22e1d-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="22e1d-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22e1d-112">Prerequisites</span></span>

<span data-ttu-id="22e1d-113">Do wykonania zadań opisanych w tym samouczku niezbędne jest spełnienie następujących wymagań wstępnych:</span><span class="sxs-lookup"><span data-stu-id="22e1d-113">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="22e1d-114">Zainstalowana najnowsza wersja [programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="22e1d-114">Installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="22e1d-115">Zainstalowana baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="22e1d-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="22e1d-116">W tym samouczku używana przykładową bazę danych AdventureWorksLT o nazwie **mySampleDatabase** z jednego z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="22e1d-116">This tutorial uses the AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="22e1d-117">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="22e1d-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="22e1d-118">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="22e1d-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="22e1d-119">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="22e1d-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="22e1d-120">Zidentyfikowano metodę wykonywanie skryptów SQL bazy danych, można użyć jednej z następujących narzędzi zapytania:</span><span class="sxs-lookup"><span data-stu-id="22e1d-120">Have identified a method to execute SQL scripts against your database, you can use one of the following query tools:</span></span>
   - <span data-ttu-id="22e1d-121">Edytor zapytań w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22e1d-121">The query editor in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="22e1d-122">Aby uzyskać więcej informacji na temat używania edytora zapytań w portalu Azure, zobacz [Connect i zapytania za pomocą edytora zapytań](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="22e1d-122">For more information on using the query editor in the Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="22e1d-123">Najnowsza wersja [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), która jest zintegrowane środowisko umożliwiające zarządzanie dowolnej infrastruktury SQL z programu SQL Server z bazą danych SQL systemu Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="22e1d-123">The newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server to SQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="22e1d-124">Najnowsza wersja [Visual Studio Code](https://code.visualstudio.com/docs), czyli edytorze graficznego kodu dla systemu Linux, macOS, i systemu Windows, który obsługuje rozszerzenia, w tym [rozszerzenia mssql](https://aka.ms/mssql-marketplace) do wykonywania zapytań programu Microsoft SQL Server Baza danych Azure SQL i usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="22e1d-124">The newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="22e1d-125">Aby uzyskać więcej informacji o usłudze Azure SQL Database za pomocą tego narzędzia, zobacz [Connect i zapytanie z kodem VS](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="22e1d-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="22e1d-126">Tworzenie bazy danych użytkowników i udzielanie uprawnień</span><span class="sxs-lookup"><span data-stu-id="22e1d-126">Create database users and grant permissions</span></span>

<span data-ttu-id="22e1d-127">Połączenia z bazą danych i tworzenie kont użytkowników przy użyciu jednej z następujących narzędzi zapytania:</span><span class="sxs-lookup"><span data-stu-id="22e1d-127">Connect to your database and create user accounts using one of the following query tools:</span></span>

- <span data-ttu-id="22e1d-128">Edytor zapytań w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="22e1d-128">The Query editor in the Azure portal</span></span>
- <span data-ttu-id="22e1d-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="22e1d-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="22e1d-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="22e1d-130">Visual Studio Code</span></span>

<span data-ttu-id="22e1d-131">Te konta użytkowników automatycznie replikowane na serwerze pomocniczym (i być utrzymywane w synchronizacji).</span><span class="sxs-lookup"><span data-stu-id="22e1d-131">These user accounts replicate automatically to your secondary server (and be kept in sync).</span></span> <span data-ttu-id="22e1d-132">Aby użyć programu SQL Server Management Studio lub Visual Studio Code, może być konieczne skonfigurowanie reguły zapory, jeśli łączysz się z adresem IP, dla którego nie została jeszcze skonfigurowana zapora klienta.</span><span class="sxs-lookup"><span data-stu-id="22e1d-132">To use SQL Server Management Studio or Visual Studio Code, you may need to configure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="22e1d-133">Aby uzyskać szczegółowe instrukcje, zobacz [utworzyć regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="22e1d-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="22e1d-134">W oknie zapytania wykonaj następujące zapytanie, aby utworzyć dwa konta użytkownika w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="22e1d-134">In a query window, execute the following query to create two user accounts in your database.</span></span> <span data-ttu-id="22e1d-135">Ten skrypt przyznaje **db_owner** uprawnień do **app_admin** konto i przyznaje **wybierz** i **aktualizacji** uprawnień do **app_user** konta.</span><span class="sxs-lookup"><span data-stu-id="22e1d-135">This script grants **db_owner** permissions to the **app_admin** account and grants **SELECT** and **UPDATE** permissions to the **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user to db_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission to SalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product TO app_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="22e1d-136">Utwórz zapory poziomu bazy danych</span><span class="sxs-lookup"><span data-stu-id="22e1d-136">Create database-level firewall</span></span>

<span data-ttu-id="22e1d-137">Utwórz [reguły zapory poziomu bazy danych](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="22e1d-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="22e1d-138">Tę regułę zapory poziomu bazy danych automatycznie replikuje dane na serwerze pomocniczym, utworzone w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="22e1d-138">This database-level firewall rule replicates automatically to the secondary server that you create in this tutorial.</span></span> <span data-ttu-id="22e1d-139">Dla uproszczenia (w tym samouczku) Użyj publiczny adres IP komputera, na którym wykonywana kroki opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="22e1d-139">For simplicity (in this tutorial), use the public IP address of the computer on which you are performing the steps in this tutorial.</span></span> <span data-ttu-id="22e1d-140">Aby określić adres IP używany dla reguły zapory poziomu serwera dla bieżącego komputera, zobacz [utworzenie zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="22e1d-140">To determine the IP address used for the server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="22e1d-141">W oknie zapytania otwarte należy zastąpić poprzednie zapytanie następującej kwerendy, zastępując adresy IP odpowiednie adresy IP dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="22e1d-141">In your open query window, replace the previous query with the following query, replacing the IP addresses with the appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="22e1d-142">Utwórz grupę aktywna replikacja geograficzna automatycznej pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="22e1d-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="22e1d-143">Przy użyciu programu Azure PowerShell utworzyć [aktywna replikacja geograficzna automatycznej pracy awaryjnej grupy](sql-database-geo-replication-overview.md) między istniejącego serwera Azure SQL i nowy pusty serwera Azure SQL w regionie Azure, a następnie dodaj przykładowej bazie danych do trybu failover grupy.</span><span class="sxs-lookup"><span data-stu-id="22e1d-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and the new empty Azure SQL server in an Azure region, and then add your sample database to the failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22e1d-144">Te polecenia cmdlet wymagają programu Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="22e1d-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="22e1d-145">Wypełnić zmienne dla skryptów PowerShell przy użyciu wartości dla istniejącego serwera i przykładową bazę danych i podaj globalnie unikatowa wartość nazwy grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="22e1d-145">Populate variables for your PowerShell scripts using the values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

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

2. <span data-ttu-id="22e1d-146">W danym regionie trybu failover, należy utworzyć pusty serwer kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="22e1d-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="22e1d-147">Utwórz grupę trybu failover między dwoma serwerami.</span><span class="sxs-lookup"><span data-stu-id="22e1d-147">Create a failover group between the two servers.</span></span>

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

4. <span data-ttu-id="22e1d-148">Dodaj bazę danych do grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="22e1d-148">Add your database to the failover group.</span></span>

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

## <a name="install-java-software"></a><span data-ttu-id="22e1d-149">Instalowanie oprogramowania Java</span><span class="sxs-lookup"><span data-stu-id="22e1d-149">Install Java software</span></span>

<span data-ttu-id="22e1d-150">W krokach w tej sekcji założono, że wiesz już, jak opracowywać zawartość za pomocą platformy Java, i dopiero zaczynasz pracę z usługą Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="22e1d-150">The steps in this section assume that you are familiar with developing using Java and are new to working with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="22e1d-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="22e1d-151">**Mac OS**</span></span>
<span data-ttu-id="22e1d-152">Otwórz terminal i przejdź do katalogu, w którym planujesz utworzyć projekt języka Java.</span><span class="sxs-lookup"><span data-stu-id="22e1d-152">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="22e1d-153">Zainstaluj rozwiązania **brew** i **Maven** przez wprowadzenie następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="22e1d-153">Install **brew** and **Maven** by entering the following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="22e1d-154">Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję **MacOS**i postępuj szczegółowe instrukcje dotyczące konfigurowania Java i Maven w kroku 1.2 i 1.3.</span><span class="sxs-lookup"><span data-stu-id="22e1d-154">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="22e1d-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="22e1d-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="22e1d-156">Otwórz terminal i przejdź do katalogu, w którym planujesz utworzyć projekt języka Java.</span><span class="sxs-lookup"><span data-stu-id="22e1d-156">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="22e1d-157">Zainstaluj rozwiązanie **Maven** przez wprowadzenie następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="22e1d-157">Install **Maven** by entering the following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="22e1d-158">Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję **Ubuntu**i postępuj szczegółowe instrukcje dotyczące konfigurowania Java i Maven w kroku 1.2, 1.3 i 1.4.</span><span class="sxs-lookup"><span data-stu-id="22e1d-158">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow the detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="22e1d-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="22e1d-159">**Windows**</span></span>
<span data-ttu-id="22e1d-160">Zainstaluj rozwiązanie [Maven](https://maven.apache.org/download.cgi) za pomocą oficjalnego instalatora.</span><span class="sxs-lookup"><span data-stu-id="22e1d-160">Install [Maven](https://maven.apache.org/download.cgi) using the official installer.</span></span> <span data-ttu-id="22e1d-161">Użyj Maven, aby ułatwić zarządzanie zależności, tworzenia, testowania i uruchom projekt języka Java.</span><span class="sxs-lookup"><span data-stu-id="22e1d-161">Use Maven to help manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="22e1d-162">Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**wybierz systemu Windows, a następnie postępuj zgodnie z instrukcjami szczegółowe Konfigurowanie języka Java i Maven w kroku 1.2 i 1.3.</span><span class="sxs-lookup"><span data-stu-id="22e1d-162">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="22e1d-163">Utwórz projekt SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="22e1d-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="22e1d-164">W konsoli poleceń (na przykład Bash) Utwórz projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="22e1d-164">In the command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="22e1d-165">Typ **Y** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="22e1d-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="22e1d-166">Przejdź do nowo utworzonego projektu.</span><span class="sxs-lookup"><span data-stu-id="22e1d-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="22e1d-167">Za pomocą ulubionego edytora, otwórz plik pom.xml w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="22e1d-167">Using your favorite editor, open the pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="22e1d-168">Dodaj sterownik JDBC firmy Microsoft dla programu SQL Server zależności na projekt Maven przez otwarcie w ulubionym edytorze tekstów i kopiowanie i wklejanie następujące wiersze w pliku pom.xml.</span><span class="sxs-lookup"><span data-stu-id="22e1d-168">Add the Microsoft JDBC Driver for SQL Server dependency to your Maven project by opening your favorite text editor and copying and pasting the following lines into your pom.xml file.</span></span> <span data-ttu-id="22e1d-169">Nie zastępuj istniejącego wartości wstępnie w pliku.</span><span class="sxs-lookup"><span data-stu-id="22e1d-169">Do not overwrite the existing values prepopulated in the file.</span></span> <span data-ttu-id="22e1d-170">Zależności JDBC należy wkleić w większych () sekcji "zależności".</span><span class="sxs-lookup"><span data-stu-id="22e1d-170">The JDBC dependency must be pasted within the larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="22e1d-171">Określ wersję Java do skompilowania projektu w odniesieniu do, dodając w poniższej sekcji "właściwości" w pliku pom.xml po sekcji "zależności".</span><span class="sxs-lookup"><span data-stu-id="22e1d-171">Specify the version of Java to compile the project against by adding the following “properties” section into the pom.xml file after the "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="22e1d-172">Dodaj poniższą sekcję "kompilacji" w pliku pom.xml po sekcji "właściwości" do obsługi plików manifestu w słoików.</span><span class="sxs-lookup"><span data-stu-id="22e1d-172">Add the following "build" section into the pom.xml file after the "properties" section to support manifest files in jars.</span></span>       

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
8. <span data-ttu-id="22e1d-173">Zapisz i zamknij plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="22e1d-173">Save and close the pom.xml file.</span></span>
9. <span data-ttu-id="22e1d-174">Otwórz plik App.java (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) i Zastąp zawartość następującą zawartość.</span><span class="sxs-lookup"><span data-stu-id="22e1d-174">Open the App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace the contents with the following contents.</span></span> <span data-ttu-id="22e1d-175">Nazwa grupy pracy awaryjnej należy zastąpić nazwę grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="22e1d-175">Replace the failover group name with the name for your failover group.</span></span> <span data-ttu-id="22e1d-176">Zmiana wartości dla nazwy bazy danych użytkownika lub hasło, należy zmienić również tych wartości.</span><span class="sxs-lookup"><span data-stu-id="22e1d-176">If you have changed the values for the database name, user, or password, change those values as well.</span></span>

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
      // Insert data into the product table with a unique product name that we can use to find the product again later
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
      // Query the data that was previously inserted into the primary database from the geo replicated database
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
      // Query the high water mark id that is stored in the table to be able to make unique inserts 
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
6. <span data-ttu-id="22e1d-177">Zapisz i zamknij plik App.java.</span><span class="sxs-lookup"><span data-stu-id="22e1d-177">Save and close the App.java file.</span></span>

## <a name="compile-and-run-the-sqldbsample-project"></a><span data-ttu-id="22e1d-178">Kompilowanie i uruchamianie projektu SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="22e1d-178">Compile and run the SqlDbSample project</span></span>

1. <span data-ttu-id="22e1d-179">W konsoli polecenie należy wykonać następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="22e1d-179">In the command console, execute to following command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="22e1d-180">Po zakończeniu uruchom następujące polecenie do uruchomienia aplikacji (działa na godzinę, chyba że zostanie zatrzymana ręcznie):</span><span class="sxs-lookup"><span data-stu-id="22e1d-180">When finished, execute the following command to run the application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="22e1d-181">Wykonaj wyszczególniania odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="22e1d-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="22e1d-182">Wywołanie ręcznego przełączania trybu failover grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="22e1d-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="22e1d-183">Obserwować wyniki aplikacji podczas pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="22e1d-183">Observe the application results during failover.</span></span> <span data-ttu-id="22e1d-184">Niektóre wstawia się niepowodzeniem podczas odświeżania pamięci podręcznej DNS.</span><span class="sxs-lookup"><span data-stu-id="22e1d-184">Some inserts fail while the DNS cache refreshes.</span></span>     

3. <span data-ttu-id="22e1d-185">Dowiedz się od roli działa serwer odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="22e1d-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="22e1d-186">Powrót po awarii.</span><span class="sxs-lookup"><span data-stu-id="22e1d-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="22e1d-187">Obserwować wyniki aplikacji podczas powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="22e1d-187">Observe the application results during failback.</span></span> <span data-ttu-id="22e1d-188">Niektóre wstawia się niepowodzeniem podczas odświeżania pamięci podręcznej DNS.</span><span class="sxs-lookup"><span data-stu-id="22e1d-188">Some inserts fail while the DNS cache refreshes.</span></span>     

6. <span data-ttu-id="22e1d-189">Dowiedz się od roli działa serwer odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="22e1d-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="22e1d-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22e1d-190">Next steps</span></span> 

<span data-ttu-id="22e1d-191">Aby uzyskać więcej informacji, zobacz [aktywnych grup — replikacja geograficzna i pracy awaryjnej](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22e1d-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
