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
# <a name="create-a-single-azure-sql-database-using-powershell"></a>Tworzenie pojedynczej bazy danych Azure SQL Database za pomocą programu PowerShell

PowerShell jest używane toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Ten przewodnik szczegółów przy użyciu programu PowerShell toodeploy bazy danych Azure SQL w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w [serwera logicznego bazy danych SQL Azure](sql-database-features.md).

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

Ten samouczek wymaga hello Azure PowerShell modułu w wersji 4.0 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za tooyour subskrypcji platformy Azure przy użyciu hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) poleceń i wykonaj hello wyświetlanymi instrukcjami.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Tworzenie zmiennych

Zdefiniuj zmienne do użytku w skryptach hello w tym szybki start.

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

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia. Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>Tworzenie serwera logicznego

Utwórz [serwera logicznego bazy danych SQL Azure](sql-database-features.md) przy użyciu hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) polecenia. Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa. Witaj poniższy przykład tworzy losowo nazwanym serwerze w grupie zasobów o nazwie identyfikator logowania administratora `ServerAdmin` oraz hasła `ChangeYourAdminPassword1`. Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Konfigurowanie reguły zapory serwera

Utwórz [regułę zapory poziomu serwera bazy danych SQL Azure](sql-database-firewall-configure.md) przy użyciu hello [AzureRmSqlServerFirewallRule nowy](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) polecenia. Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak SQL Server Management Studio lub hello SQLCMD narzędzie tooconnect tooa bazy danych SQL za pośrednictwem zapory usługi SQL Database hello. W hello poniższy przykład hello zapory jest otwarty tylko do innych zasobów platformy Azure. tooenable łączność zewnętrzną, zmiana hello adres tooan odpowiedniego adresu IP dla danego środowiska. tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> Usługa SQL Database nawiązuje komunikację na porcie 1433. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Utwórz bazę danych na serwerze hello z przykładowymi danymi

Utwórz bazę danych z [poziom wydajności S0](sql-database-service-tiers.md) w powitania serwera przy użyciu hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) polecenia. Witaj poniższy przykład tworzy bazę danych o nazwie `mySampleDatabase` i obciążeń hello AdventureWorksLT przykładowe dane do tej bazy danych. Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami (inne Szybkie uruchamianie w tej kolekcji kompilacji na powitania wartości w tym szybki start).

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. 

> [!TIP]
> Jeśli planujesz toocontinue toowork z kolejnych Szybki Start, nie czyszczenie zasobów hello utworzone w tym szybki start. Jeśli nie planujesz toocontinue, użyj powitania po toodelete kroki wszystkie zasoby utworzone przez tego szybkiego startu w portalu Azure hello.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Następne kroki

Teraz, gdy już masz bazę danych, możesz nawiązać z nią połączenie i uruchamiać zapytania za pomocą ulubionych narzędzi. Dowiedz się więcej, wybierając narzędzie poniżej:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

