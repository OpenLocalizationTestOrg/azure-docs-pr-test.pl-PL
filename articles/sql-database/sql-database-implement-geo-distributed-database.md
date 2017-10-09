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
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="8fb6a-103">Wdrożenie rozproszone geograficznie bazy danych</span><span class="sxs-lookup"><span data-stu-id="8fb6a-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="8fb6a-104">W tym samouczku skonfiguruj bazy danych Azure SQL i aplikacji dla trybu failover tooa zdalnego regionu, a następnie testować tryb failover planu.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="8fb6a-105">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="8fb6a-106">Tworzenie bazy danych użytkowników i udzielić im uprawnień</span><span class="sxs-lookup"><span data-stu-id="8fb6a-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="8fb6a-107">Skonfiguruj regułę zapory poziomu bazy danych</span><span class="sxs-lookup"><span data-stu-id="8fb6a-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="8fb6a-108">Utwórz [— replikacja geograficzna trybu failover grupy](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8fb6a-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="8fb6a-109">Tworzenie i kompilacja tooquery aplikacji Java bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="8fb6a-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="8fb6a-110">Wykonaj wyszczególniania odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="8fb6a-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="8fb6a-111">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8fb6a-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8fb6a-112">Prerequisites</span></span>

<span data-ttu-id="8fb6a-113">toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="8fb6a-114">Najnowsza wersja zainstalowanego hello [programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="8fb6a-115">Zainstalowana baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="8fb6a-116">W tym samouczku używana hello AdventureWorksLT przykładowa baza danych o nazwie **mySampleDatabase** z jednego z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="8fb6a-117">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="8fb6a-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8fb6a-118">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="8fb6a-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8fb6a-119">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fb6a-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8fb6a-120">Zidentyfikowano tooexecute metody SQL skryptów bazy danych, można użyć jednej z hello następujące narzędzia kwerendy:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="8fb6a-121">Edytor zapytań Hello w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8fb6a-122">Aby uzyskać więcej informacji na temat używania edytora zapytań hello w hello portalu Azure, zobacz [Connect i zapytania za pomocą edytora zapytań](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="8fb6a-123">Witaj najnowsza wersja [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), która jest zintegrowane środowisko umożliwiające zarządzanie dowolnej infrastruktury SQL z programu SQL Server tooSQL bazy danych systemu Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="8fb6a-124">Hello najnowsza wersja [Visual Studio Code](https://code.visualstudio.com/docs), czyli edytorze graficznego kodu dla systemu Linux, macOS, i systemu Windows, które obsługuje rozszerzenia, w tym hello [rozszerzenia mssql](https://aka.ms/mssql-marketplace) do wykonywania zapytań programu Microsoft SQL Server , Baza danych azure SQL i SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="8fb6a-125">Aby uzyskać więcej informacji o usłudze Azure SQL Database za pomocą tego narzędzia, zobacz [Connect i zapytanie z kodem VS](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="8fb6a-126">Tworzenie bazy danych użytkowników i udzielanie uprawnień</span><span class="sxs-lookup"><span data-stu-id="8fb6a-126">Create database users and grant permissions</span></span>

<span data-ttu-id="8fb6a-127">Łączenie tooyour bazy danych i tworzenie kont użytkowników przy użyciu jednej z hello następujące narzędzia kwerendy:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="8fb6a-128">Edytor zapytań Hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8fb6a-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="8fb6a-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="8fb6a-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="8fb6a-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8fb6a-130">Visual Studio Code</span></span>

<span data-ttu-id="8fb6a-131">Te konta użytkowników automatycznie replikowane tooyour pomocniczy serwer (i są synchronizowane).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="8fb6a-132">toouse SQL Server Management Studio lub Visual Studio Code, jeśli nawiązujesz połączenie z klienta na adres IP, dla którego nie została jeszcze skonfigurowana zapora może być konieczne tooconfigure reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="8fb6a-133">Aby uzyskać szczegółowe instrukcje, zobacz [utworzyć regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="8fb6a-134">W oknie zapytania należy wykonać hello następującego zapytania toocreate dwóch kont użytkownika w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="8fb6a-135">Ten skrypt przyznaje **db_owner** toohello uprawnienia **app_admin** konto i przyznaje **wybierz** i **aktualizacji** toohello uprawnień **app_user** konta.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="8fb6a-136">Utwórz zapory poziomu bazy danych</span><span class="sxs-lookup"><span data-stu-id="8fb6a-136">Create database-level firewall</span></span>

<span data-ttu-id="8fb6a-137">Utwórz [reguły zapory poziomu bazy danych](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="8fb6a-138">Ta reguła zapory poziomu bazy danych automatycznie replikuje toohello serwera pomocniczego, utworzone w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="8fb6a-139">Dla uproszczenia (w tym samouczku) Użyj publicznego adresu IP hello hello komputera, na którym hello kroki są wykonywane w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="8fb6a-140">adres IP hello toodetermine używany dla reguły zapory poziomu serwera hello na tym samym komputerze, zobacz [utworzenie zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="8fb6a-141">W oknie zapytania otwarte należy zastąpić poprzednie zapytanie hello hello następującego zapytania, zastępując adresy IP hello hello odpowiednie adresy IP dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="8fb6a-142">Utwórz grupę aktywna replikacja geograficzna automatycznej pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="8fb6a-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="8fb6a-143">Przy użyciu programu Azure PowerShell utworzyć [aktywna replikacja geograficzna automatycznej pracy awaryjnej grupy](sql-database-geo-replication-overview.md) między istniejącego serwera Azure SQL i hello nowy pusty serwera Azure SQL w regionie Azure, a następnie dodaj grupy pracy awaryjnej toohello przykładowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fb6a-144">Te polecenia cmdlet wymagają programu Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="8fb6a-145">Wypełnić zmienne dla skryptów PowerShell przy użyciu wartości hello istniejącego serwera i przykładową bazę danych i podaj globalnie unikatowa wartość nazwy grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

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

2. <span data-ttu-id="8fb6a-146">W danym regionie trybu failover, należy utworzyć pusty serwer kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="8fb6a-147">Utwórz grupę trybu failover między dwoma serwerami hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-147">Create a failover group between hello two servers.</span></span>

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

4. <span data-ttu-id="8fb6a-148">Dodaj grupy pracy awaryjnej toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-148">Add your database toohello failover group.</span></span>

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

## <a name="install-java-software"></a><span data-ttu-id="8fb6a-149">Instalowanie oprogramowania Java</span><span class="sxs-lookup"><span data-stu-id="8fb6a-149">Install Java software</span></span>

<span data-ttu-id="8fb6a-150">kroki Hello w tej sekcji założono, że znasz tworzenie przy użyciu języka Java i są nowe tooworking z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="8fb6a-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="8fb6a-151">**Mac OS**</span></span>
<span data-ttu-id="8fb6a-152">Otwórz terminala i przejdź do katalogu tooa, w którym planujesz utworzenie projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="8fb6a-153">Zainstaluj **brew** i **Maven** wprowadzając hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="8fb6a-154">Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź hello [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję **MacOS**i postępuj Witaj szczegółowe instrukcje dotyczące konfigurowania Java i Maven w kroku 1.2 i 1.3.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="8fb6a-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="8fb6a-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="8fb6a-156">Otwórz terminala i przejdź do katalogu tooa, w którym planujesz utworzenie projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="8fb6a-157">Zainstaluj **Maven** wprowadzając hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8fb6a-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="8fb6a-158">Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź hello [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję **Ubuntu**i postępuj Witaj szczegółowe instrukcje dotyczące konfigurowania Java i Maven w kroku 1.2, 1.3 i 1.4.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="8fb6a-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="8fb6a-159">**Windows**</span></span>
<span data-ttu-id="8fb6a-160">Zainstaluj [Maven](https://maven.apache.org/download.cgi) za pomocą Instalatora oficjalnego hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="8fb6a-161">Używanie programu Maven toohelp Zarządzanie zależności, tworzenia, testowania i uruchom projekt języka Java.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="8fb6a-162">Aby uzyskać szczegółowe instrukcje dotyczące instalowania i konfigurowania środowiska Java i Maven, przejdź hello [tworzenie aplikacji za pomocą programu SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), wybierz pozycję **Java**, wybierz pozycję Windows, a następnie wykonaj hello szczegółowe instrukcje dotyczące Konfigurowanie języka Java i Maven w kroku 1.2 i 1.3.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="8fb6a-163">Utwórz projekt SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="8fb6a-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="8fb6a-164">W konsoli polecenie hello (na przykład Bash) Utwórz projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="8fb6a-165">Typ **Y** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="8fb6a-166">Przejdź do nowo utworzonego projektu.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="8fb6a-167">Za pomocą ulubionego edytora, otwórz plik pom.xml hello w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="8fb6a-168">Dodaj hello sterownik JDBC firmy Microsoft dla programu SQL Server zależności tooyour Maven project przez otwarcie w ulubionym edytorze tekstów i kopiowanie i wklejanie hello następujące wiersze do pliku pom.xml.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="8fb6a-169">Nie zastępuj istniejące wartości hello wypełniony hello pliku.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="8fb6a-170">Hello zależności JDBC należy wkleić w ciągu (hello większych "zależności" sekcji).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="8fb6a-171">Określ wersję hello Java toocompile hello projektu w odniesieniu do przez dodanie powitania po sekcji "właściwości" w pliku pom.xml powitania po sekcji "zależności" hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="8fb6a-172">Dodaj następujące hello "kompilacji" sekcji w pliku pom.xml powitania po hello "właściwości" sekcji toosupport pliki manifestu w słoików.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

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
8. <span data-ttu-id="8fb6a-173">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="8fb6a-174">Otwórz plik App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) i Zastąp zawartość hello powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="8fb6a-175">Zastąp nazwę grupy pracy awaryjnej hello hello nazwę grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="8fb6a-176">Zmiana wartości hello hello Nazwa bazy danych użytkownika lub hasło, należy zmienić także te wartości.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

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
6. <span data-ttu-id="8fb6a-177">Zapisz i zamknij plik App.java hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="8fb6a-178">Kompilowanie i uruchamianie projektu SqlDbSample hello</span><span class="sxs-lookup"><span data-stu-id="8fb6a-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="8fb6a-179">W konsoli poleceń hello wykonaj polecenie toofollowing.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="8fb6a-180">Po zakończeniu wykonywania powitania po aplikacji hello toorun poleceń (działa na godzinę, chyba że zostanie zatrzymana ręcznie):</span><span class="sxs-lookup"><span data-stu-id="8fb6a-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="8fb6a-181">Wykonaj wyszczególniania odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="8fb6a-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="8fb6a-182">Wywołanie ręcznego przełączania trybu failover grupy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="8fb6a-183">Obserwować wyniki aplikacji hello, podczas pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-183">Observe hello application results during failover.</span></span> <span data-ttu-id="8fb6a-184">Niektóre wstawia się niepowodzeniem podczas odświeżania pamięci podręcznej DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="8fb6a-185">Dowiedz się od roli działa serwer odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="8fb6a-186">Powrót po awarii.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="8fb6a-187">Należy obserwować wyniki aplikacji hello podczas powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-187">Observe hello application results during failback.</span></span> <span data-ttu-id="8fb6a-188">Niektóre wstawia się niepowodzeniem podczas odświeżania pamięci podręcznej DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="8fb6a-189">Dowiedz się od roli działa serwer odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="8fb6a-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="8fb6a-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fb6a-190">Next steps</span></span> 

<span data-ttu-id="8fb6a-191">Aby uzyskać więcej informacji, zobacz [aktywnych grup — replikacja geograficzna i pracy awaryjnej](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fb6a-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
