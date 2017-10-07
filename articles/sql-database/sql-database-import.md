---
title: aaaImport pliku BACPAC pliku toocreate bazy danych Azure SQL | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="81874-103">Importuj tooa pliku pliku BACPAC nowej bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="81874-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="81874-104">Kiedy należy tooimport bazę danych z archiwum lub podczas migracji z innej platformie, możesz zaimportować hello schematu bazy danych i danych z [pliku BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) pliku.</span><span class="sxs-lookup"><span data-stu-id="81874-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="81874-105">Plik pliku BACPAC to plik ZIP z rozszerzeniem pliku BACPAC zawierające hello metadane i dane z bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="81874-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="81874-106">Można zaimportować pliku BACPAC pliku z magazynu obiektów blob platformy Azure (tylko w przypadku magazynu standard) lub z magazynu lokalnego w lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="81874-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="81874-107">toomaximize hello importu szybkości, zalecamy wyższej wydajności i warstwę poziomu usługi, takie jak P6, określ, a następnie skalować toodown odpowiednio po hello import zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="81874-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="81874-108">Ponadto hello poziom zgodności bazy danych po hello importu jest oparta na poziom zgodności hello hello źródłowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="81874-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="81874-109">Po przeprowadzeniu migracji tooAzure Twojej bazy danych SQL Database, można wybrać bazę danych hello toooperate na jego bieżący poziom zgodności (poziom 100 dla bazy danych AdventureWorks2008R2 hello) lub na wyższym poziomie.</span><span class="sxs-lookup"><span data-stu-id="81874-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="81874-110">Aby uzyskać więcej informacji na powitania wpływ i opcje dla działania bazy danych na poziomie zgodności określonego, zobacz [zmienić poziom zgodności bazy danych](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="81874-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="81874-111">Zobacz też [ALTER DATABASE CONFIGURATION zakres](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) informacji o dodatkowych ustawień na poziomie bazy danych powiązanych toocompatibility poziomów.</span><span class="sxs-lookup"><span data-stu-id="81874-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="81874-112">tooimport pliku BACPAC tooa nową bazę danych, należy najpierw utworzyć serwera logicznego bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="81874-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="81874-113">Samouczek przedstawiający sposób toomigrate programu SQL Server bazy danych tooAzure bazy danych SQL przy użyciu SQLPackage, zobacz [migracji bazy danych programu SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="81874-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="81874-114">Importuj z pliku pliku BACPAC przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="81874-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="81874-115">Ten artykuł zawiera wskazówki dotyczące tworzenia bazy danych Azure SQL z pliku pliku BACPAC przechowywanych w magazynie obiektów blob platformy Azure przy użyciu hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81874-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="81874-116">Import przy użyciu hello tylko portal Azure obsługuje importowanie pliku BACPAC plik z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="81874-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="81874-117">Witaj tooimport bazy danych przy użyciu portalu Azure, otwórz hello stron dla bazy danych i kliknij przycisk **importu** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="81874-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="81874-118">Określ hello konto magazynu i kontener i wybierz plik pliku BACPAC hello ma tooimport.</span><span class="sxs-lookup"><span data-stu-id="81874-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="81874-119">Wybierz rozmiar hello hello nowej bazy danych (zazwyczaj hello sam jako punkt początkowy) i podaj poświadczenia, hello docelowego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="81874-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Importowanie bazy danych](./media/sql-database-import/import.png)

<span data-ttu-id="81874-121">postęp hello toomonitor hello operacji importu, otwórz stronę hello powitania serwera logicznego zawierającego hello bazy danych zostały zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="81874-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="81874-122">Przewiń w dół za**operacji** , a następnie kliknij przycisk **importu/eksportu** historii.</span><span class="sxs-lookup"><span data-stu-id="81874-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="81874-123">Monitoruj postęp hello operacji importu</span><span class="sxs-lookup"><span data-stu-id="81874-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="81874-124">postęp hello toomonitor hello operacji importu, otwórz stronę hello powitania serwera logicznego do których hello bazy danych jest importowany zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="81874-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="81874-125">Przewiń w dół za**operacji** , a następnie kliknij przycisk **importu/eksportu** historii.</span><span class="sxs-lookup"><span data-stu-id="81874-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="81874-126">![Importuj](./media/sql-database-import/import-history.png) ![stan importowania](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="81874-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="81874-127">Baza danych hello tooverify znajduje się na żywo na powitania serwera, kliknij przycisk **baz danych programu SQL** i sprawdź hello nowej bazy danych jest **Online**.</span><span class="sxs-lookup"><span data-stu-id="81874-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="81874-128">Importuj z pliku pliku BACPAC przy użyciu SQLPackage</span><span class="sxs-lookup"><span data-stu-id="81874-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="81874-129">tooimport SQL bazy danych przy użyciu hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) narzędzie wiersza polecenia, zobacz [zaimportować parametrów i właściwości](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="81874-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="81874-130">Narzędzie SQLPackage Hello jest dostarczany z hello najnowsze wersje [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) i [programu SQL Server Data Tools dla programu Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), lub hello najnowszą wersję można pobrać [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) bezpośrednio z hello Microsoft Centrum pobierania.</span><span class="sxs-lookup"><span data-stu-id="81874-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="81874-131">Firma Microsoft zaleca użycie hello hello narzędzie SQLPackage na skalowalność i wydajność w większości środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="81874-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="81874-132">Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="81874-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="81874-133">Zobacz hello następujące polecenia SQLPackage, na przykład skryptu, jak tooimport hello **AdventureWorks2008R2** bazy danych z magazynu lokalnego tooan bazy danych SQL Azure serwer logiczny, nazywany **mynewserver20170403** w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="81874-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="81874-134">Ten skrypt pokazuje hello Tworzenie nowej bazy danych o nazwie **myMigratedDatabase**, z warstwy usług z **Premium**, a celem usługi **P6**.</span><span class="sxs-lookup"><span data-stu-id="81874-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="81874-135">Zmień wartości tych jako odpowiednie tooyour środowiska.</span><span class="sxs-lookup"><span data-stu-id="81874-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![Importuj sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="81874-137">Serwer logiczny usługi Azure SQL Database nasłuchuje na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="81874-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="81874-138">Jeśli próbujesz tooconnect tooan bazy danych SQL Azure serwera logicznego od w obrębie firmowej zapory, ten port musi być otwarty w hello firmowej zapory dla toosuccessfully można połączyć z usługą.</span><span class="sxs-lookup"><span data-stu-id="81874-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="81874-139">W tym przykładzie pokazano sposób tooimport a bazą danych przy użyciu SqlPackage.exe z uniwersalnych uwierzytelnianie usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="81874-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="81874-140">Importuj z pliku pliku BACPAC przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="81874-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="81874-141">Użyj hello [AzureRmSqlDatabaseImport nowy](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) toosubmit polecenia cmdlet toohello żądanie importu bazy danych usługi baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="81874-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="81874-142">W zależności od wielkości hello bazy danych hello operacji importowania może potrwać niektórych toocomplete czasu.</span><span class="sxs-lookup"><span data-stu-id="81874-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

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

<span data-ttu-id="81874-143">Stan hello toocheck hello żądania importowania, użyj hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="81874-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="81874-144">Uruchomiona natychmiast po hello żądania zwykle zwraca **stan: w toku**.</span><span class="sxs-lookup"><span data-stu-id="81874-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="81874-145">Po wyświetleniu **stanu: zakończyło się pomyślnie** hello Importowanie zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="81874-145">When you see **Status: Succeeded** hello import is complete.</span></span>

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
<span data-ttu-id="81874-146">Na przykład innego skryptu, zobacz [zaimportować bazę danych z pliku pliku BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="81874-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81874-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="81874-147">Next steps</span></span>
* <span data-ttu-id="81874-148">toolearn tooconnect tooand zapytania importowanych bazy danych SQL, zobacz [uzyskuj tooSQL bazy danych programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="81874-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="81874-149">Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="81874-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="81874-150">Omówienie hello całego programu SQL Server bazy danych procesu migracji, w tym zalecenia dotyczące wydajności, zobacz [migracji tooAzure bazy danych programu SQL Server, bazy danych SQL](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="81874-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



