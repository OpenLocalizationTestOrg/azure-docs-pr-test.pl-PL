---
title: Importowanie pliku pliku BACPAC w celu utworzenia bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: "Utwórz bazę danych SQL newAzure przez zaimportowanie pliku pliku BACPAC."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="3a438-103">Importowanie pliku pliku BACPAC do nowej bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3a438-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="3a438-104">Kiedy należy zaimportować bazę danych z archiwum lub podczas migracji z innej platformy, można zaimportować schematu bazy danych i danych z [pliku BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) pliku.</span><span class="sxs-lookup"><span data-stu-id="3a438-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="3a438-105">Plik pliku BACPAC to plik ZIP z rozszerzeniem pliku BACPAC zawierający metadane i dane z bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a438-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="3a438-106">Można zaimportować pliku BACPAC pliku z magazynu obiektów blob platformy Azure (tylko w przypadku magazynu standard) lub z magazynu lokalnego w lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3a438-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="3a438-107">Aby zmaksymalizować szybkość importu, firma Microsoft zaleca określić wyższej wydajności i warstwę poziomu usługi, takie jak P6, a następnie skalować w dół zgodnie z potrzebami, po pomyślnym zaimportowaniu.</span><span class="sxs-lookup"><span data-stu-id="3a438-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="3a438-108">Ponadto poziom zgodności bazy danych po zaimportowaniu opiera się na poziom zgodności źródłowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3a438-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="3a438-109">Po przeprowadzeniu migracji bazy danych do bazy danych SQL Azure, są dostępne do obsługi bazy danych na jego bieżący poziom zgodności (poziom 100 AdventureWorks2008R2 bazy danych) lub na wyższym poziomie.</span><span class="sxs-lookup"><span data-stu-id="3a438-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="3a438-110">Aby uzyskać więcej informacji na wpływ i opcje dla działania bazy danych na poziomie zgodności określonego, zobacz [zmienić poziom zgodności bazy danych](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="3a438-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="3a438-111">Zobacz też [ALTER DATABASE CONFIGURATION zakres](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) informacji o dodatkowe ustawienia bazy danych na poziomie związane z poziomy zgodności.</span><span class="sxs-lookup"><span data-stu-id="3a438-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="3a438-112">Aby zaimportować pliku BACPAC do nowej bazy danych, należy najpierw utworzyć serwera logicznego bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3a438-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="3a438-113">Samouczek pokazuje, jak przeprowadzić migrację bazy danych programu SQL Server z bazą danych SQL Azure przy użyciu SQLPackage, zobacz [migracji bazy danych programu SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="3a438-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="3a438-114">Importuj z pliku pliku BACPAC przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3a438-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="3a438-115">Ten artykuł zawiera wskazówki dotyczące tworzenia bazy danych Azure SQL z pliku pliku BACPAC przechowywane przy użyciu magazynu obiektów blob platformy Azure [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3a438-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3a438-116">Importowanie przy użyciu portalu Azure tylko obsługuje importowanie pliku BACPAC plik z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3a438-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="3a438-117">Aby zaimportować bazę danych przy użyciu portalu Azure, otwórz stronę bazy danych, a następnie kliknij przycisk **zaimportować** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="3a438-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="3a438-118">Określ konto magazynu i kontener, a następnie wybierz plik do zaimportowania pliku BACPAC.</span><span class="sxs-lookup"><span data-stu-id="3a438-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="3a438-119">Wybierz rozmiar nowej bazy danych (zazwyczaj takie same jak pochodzenia) i poświadczenia serwera SQL miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="3a438-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![Importowanie bazy danych](./media/sql-database-import/import.png)

<span data-ttu-id="3a438-121">Aby monitorować postęp operacji importowania, otwórz stronę dla serwera logicznego zawierającego bazę danych zostały zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="3a438-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="3a438-122">Przewiń w dół do **operacji** , a następnie kliknij przycisk **importu/eksportu** historii.</span><span class="sxs-lookup"><span data-stu-id="3a438-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="3a438-123">Monitoruj postęp operacji importowania</span><span class="sxs-lookup"><span data-stu-id="3a438-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="3a438-124">Aby monitorować postęp operacji importowania, otwórz stronę logicznego serwera, do którego jest importowany bazy danych zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="3a438-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="3a438-125">Przewiń w dół do **operacji** , a następnie kliknij przycisk **importu/eksportu** historii.</span><span class="sxs-lookup"><span data-stu-id="3a438-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="3a438-126">![Importuj](./media/sql-database-import/import-history.png) ![stan importowania](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="3a438-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="3a438-127">Aby sprawdzić, baza danych znajduje się na żywo na serwerze, kliknij przycisk **baz danych SQL** i sprawdź nowej bazy danych jest **Online**.</span><span class="sxs-lookup"><span data-stu-id="3a438-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="3a438-128">Importuj z pliku pliku BACPAC przy użyciu SQLPackage</span><span class="sxs-lookup"><span data-stu-id="3a438-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="3a438-129">Aby zaimportować bazę danych SQL przy użyciu [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) narzędzie wiersza polecenia, zobacz [zaimportować parametrów i właściwości](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="3a438-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="3a438-130">Narzędzie SQLPackage jest dostarczany z najnowszej wersji [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) i [programu SQL Server Data Tools dla programu Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), można również pobrać najnowszą wersję [SqlPackage ](https://www.microsoft.com/download/details.aspx?id=53876) bezpośrednio z Centrum pobierania Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a438-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="3a438-131">Firma Microsoft zaleca użycie narzędzia SQLPackage na skalowalność i wydajność w większości środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="3a438-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="3a438-132">Aby poczytać o migracji za pomocą plików BACPAC na blogu SQL Server Customer Advisory Team, zobacz [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrowanie z programu SQL Server do usługi Azure SQL Database za pomocą plików BACPAC).</span><span class="sxs-lookup"><span data-stu-id="3a438-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="3a438-133">Zobacz następujące polecenie SQLPackage na przykład skryptu dla importowanie **AdventureWorks2008R2** bazy danych z magazynu lokalnego do serwera logicznego bazy danych SQL Azure, o nazwie **mynewserver20170403** w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3a438-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="3a438-134">Ten skrypt pokazuje Tworzenie nowej bazy danych o nazwie **myMigratedDatabase**, z warstwy usług z **Premium**, a celem usługi **P6**.</span><span class="sxs-lookup"><span data-stu-id="3a438-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="3a438-135">Zmiany tych wartości odpowiednich dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="3a438-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![Importuj sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="3a438-137">Serwer logiczny usługi Azure SQL Database nasłuchuje na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="3a438-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="3a438-138">Jeśli próbujesz nawiązać połączenie z serwerem logicznym usługi Azure SQL Database za pośrednictwem zapory firmowej, to aby połączenie się powiodło, ten port musi być otwarty w zaporze firmowej.</span><span class="sxs-lookup"><span data-stu-id="3a438-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="3a438-139">W tym przykładzie pokazano, jak zaimportować bazę danych przy użyciu SqlPackage.exe z uniwersalnych uwierzytelnianie usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="3a438-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="3a438-140">Importuj z pliku pliku BACPAC przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a438-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="3a438-141">Użyj [AzureRmSqlDatabaseImport nowy](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) polecenia cmdlet, aby przesłać żądanie importu bazy danych do usługi baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3a438-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="3a438-142">W zależności od rozmiaru bazy danych operacji importowania może potrwać trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="3a438-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="3a438-143">Aby sprawdzić stan żądania importu, należy użyć [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a438-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="3a438-144">Uruchomiona natychmiast po odebraniu żądania zwykle zwraca **stan: w toku**.</span><span class="sxs-lookup"><span data-stu-id="3a438-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="3a438-145">Po wyświetleniu **stanu: zakończyło się pomyślnie** Importowanie zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="3a438-145">When you see **Status: Succeeded** the import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="3a438-146">Na przykład innego skryptu, zobacz [zaimportować bazę danych z pliku pliku BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3a438-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a438-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a438-147">Next steps</span></span>
* <span data-ttu-id="3a438-148">Aby dowiedzieć się, jak nawiązać połączenie i zapytanie importowanych bazy danych SQL, zobacz [Połącz z bazą danych SQL za pomocą programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="3a438-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="3a438-149">Aby poczytać o migracji za pomocą plików BACPAC na blogu SQL Server Customer Advisory Team, zobacz [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrowanie z programu SQL Server do usługi Azure SQL Database za pomocą plików BACPAC).</span><span class="sxs-lookup"><span data-stu-id="3a438-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="3a438-150">Omówienie całego programu SQL Server bazy danych procesu migracji, w tym zalecenia dotyczące wydajności, zobacz [migrację bazy danych programu SQL Server do bazy danych SQL Azure](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="3a438-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



