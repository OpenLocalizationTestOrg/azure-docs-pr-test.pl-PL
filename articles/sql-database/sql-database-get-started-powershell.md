---
title: 'Azure PowerShell: tworzenie bazy danych SQL | Microsoft Docs'
description: "Dowiedz się, jak toocreate serwera logicznego SQL Database, regułę zapory poziomu serwera i bazy danych w hello portalu Azure."
keywords: "samouczek usługi sql database, tworzenie bazy danych sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="0b184-104">Tworzenie pojedynczej bazy danych Azure SQL Database za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b184-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="0b184-105">PowerShell jest używane toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="0b184-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="0b184-106">Ten przewodnik szczegółów przy użyciu programu PowerShell toodeploy bazy danych Azure SQL w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w [serwera logicznego bazy danych SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="0b184-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="0b184-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="0b184-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="0b184-108">Ten samouczek wymaga hello Azure PowerShell modułu w wersji 4.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0b184-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="0b184-109">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="0b184-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="0b184-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0b184-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="0b184-111">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="0b184-111">Log in tooAzure</span></span>

<span data-ttu-id="0b184-112">Zaloguj się za tooyour subskrypcji platformy Azure przy użyciu hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="0b184-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="0b184-113">Tworzenie zmiennych</span><span class="sxs-lookup"><span data-stu-id="0b184-113">Create variables</span></span>

<span data-ttu-id="0b184-114">Zdefiniuj zmienne do użytku w skryptach hello w tym szybki start.</span><span class="sxs-lookup"><span data-stu-id="0b184-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0b184-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="0b184-115">Create a resource group</span></span>

<span data-ttu-id="0b184-116">Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0b184-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="0b184-117">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="0b184-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="0b184-118">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0b184-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="0b184-119">Tworzenie serwera logicznego</span><span class="sxs-lookup"><span data-stu-id="0b184-119">Create a logical server</span></span>

<span data-ttu-id="0b184-120">Utwórz [serwera logicznego bazy danych SQL Azure](sql-database-features.md) przy użyciu hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0b184-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="0b184-121">Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="0b184-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="0b184-122">Witaj poniższy przykład tworzy losowo nazwanym serwerze w grupie zasobów o nazwie identyfikator logowania administratora `ServerAdmin` oraz hasła `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="0b184-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="0b184-123">Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="0b184-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="0b184-124">Konfigurowanie reguły zapory serwera</span><span class="sxs-lookup"><span data-stu-id="0b184-124">Configure a server firewall rule</span></span>

<span data-ttu-id="0b184-125">Utwórz [regułę zapory poziomu serwera bazy danych SQL Azure](sql-database-firewall-configure.md) przy użyciu hello [AzureRmSqlServerFirewallRule nowy](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0b184-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="0b184-126">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak SQL Server Management Studio lub hello SQLCMD narzędzie tooconnect tooa bazy danych SQL za pośrednictwem zapory usługi SQL Database hello.</span><span class="sxs-lookup"><span data-stu-id="0b184-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="0b184-127">W hello poniższy przykład hello zapory jest otwarty tylko do innych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b184-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="0b184-128">tooenable łączność zewnętrzną, zmiana hello adres tooan odpowiedniego adresu IP dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="0b184-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="0b184-129">tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.</span><span class="sxs-lookup"><span data-stu-id="0b184-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="0b184-130">Usługa SQL Database nawiązuje komunikację na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="0b184-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="0b184-131">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="0b184-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0b184-132">Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 1433.</span><span class="sxs-lookup"><span data-stu-id="0b184-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="0b184-133">Utwórz bazę danych na serwerze hello z przykładowymi danymi</span><span class="sxs-lookup"><span data-stu-id="0b184-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="0b184-134">Utwórz bazę danych z [poziom wydajności S0](sql-database-service-tiers.md) w powitania serwera przy użyciu hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0b184-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="0b184-135">Witaj poniższy przykład tworzy bazę danych o nazwie `mySampleDatabase` i obciążeń hello AdventureWorksLT przykładowe dane do tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0b184-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="0b184-136">Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami (inne Szybkie uruchamianie w tej kolekcji kompilacji na powitania wartości w tym szybki start).</span><span class="sxs-lookup"><span data-stu-id="0b184-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="0b184-137">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="0b184-137">Clean up resources</span></span>

<span data-ttu-id="0b184-138">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="0b184-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="0b184-139">Jeśli planujesz toocontinue toowork z kolejnych Szybki Start, nie czyszczenie zasobów hello utworzone w tym szybki start.</span><span class="sxs-lookup"><span data-stu-id="0b184-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="0b184-140">Jeśli nie planujesz toocontinue, użyj powitania po toodelete kroki wszystkie zasoby utworzone przez tego szybkiego startu w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0b184-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="0b184-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b184-141">Next steps</span></span>

<span data-ttu-id="0b184-142">Teraz, gdy już masz bazę danych, możesz nawiązać z nią połączenie i uruchamiać zapytania za pomocą ulubionych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="0b184-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="0b184-143">Dowiedz się więcej, wybierając narzędzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="0b184-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="0b184-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="0b184-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="0b184-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0b184-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="0b184-146">.NET</span><span class="sxs-lookup"><span data-stu-id="0b184-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="0b184-147">PHP</span><span class="sxs-lookup"><span data-stu-id="0b184-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="0b184-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="0b184-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="0b184-149">Java</span><span class="sxs-lookup"><span data-stu-id="0b184-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="0b184-150">Python</span><span class="sxs-lookup"><span data-stu-id="0b184-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="0b184-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="0b184-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

