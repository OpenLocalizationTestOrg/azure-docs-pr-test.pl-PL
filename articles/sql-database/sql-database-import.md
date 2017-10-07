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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Importuj tooa pliku pliku BACPAC nowej bazy danych SQL Azure

Kiedy należy tooimport bazę danych z archiwum lub podczas migracji z innej platformie, możesz zaimportować hello schematu bazy danych i danych z [pliku BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) pliku. Plik pliku BACPAC to plik ZIP z rozszerzeniem pliku BACPAC zawierające hello metadane i dane z bazy danych programu SQL Server. Można zaimportować pliku BACPAC pliku z magazynu obiektów blob platformy Azure (tylko w przypadku magazynu standard) lub z magazynu lokalnego w lokalizacji lokalnej. toomaximize hello importu szybkości, zalecamy wyższej wydajności i warstwę poziomu usługi, takie jak P6, określ, a następnie skalować toodown odpowiednio po hello import zakończy się pomyślnie. Ponadto hello poziom zgodności bazy danych po hello importu jest oparta na poziom zgodności hello hello źródłowej bazy danych. 

> [!IMPORTANT] 
> Po przeprowadzeniu migracji tooAzure Twojej bazy danych SQL Database, można wybrać bazę danych hello toooperate na jego bieżący poziom zgodności (poziom 100 dla bazy danych AdventureWorks2008R2 hello) lub na wyższym poziomie. Aby uzyskać więcej informacji na powitania wpływ i opcje dla działania bazy danych na poziomie zgodności określonego, zobacz [zmienić poziom zgodności bazy danych](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Zobacz też [ALTER DATABASE CONFIGURATION zakres](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) informacji o dodatkowych ustawień na poziomie bazy danych powiązanych toocompatibility poziomów.   >

> [!NOTE]
> tooimport pliku BACPAC tooa nową bazę danych, należy najpierw utworzyć serwera logicznego bazy danych SQL Azure. Samouczek przedstawiający sposób toomigrate programu SQL Server bazy danych tooAzure bazy danych SQL przy użyciu SQLPackage, zobacz [migracji bazy danych programu SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importuj z pliku pliku BACPAC przy użyciu portalu Azure

Ten artykuł zawiera wskazówki dotyczące tworzenia bazy danych Azure SQL z pliku pliku BACPAC przechowywanych w magazynie obiektów blob platformy Azure przy użyciu hello [portalu Azure](https://portal.azure.com). Import przy użyciu hello tylko portal Azure obsługuje importowanie pliku BACPAC plik z magazynu obiektów blob platformy Azure.

Witaj tooimport bazy danych przy użyciu portalu Azure, otwórz hello stron dla bazy danych i kliknij przycisk **importu** na powitania narzędzi. Określ hello konto magazynu i kontener i wybierz plik pliku BACPAC hello ma tooimport. Wybierz rozmiar hello hello nowej bazy danych (zazwyczaj hello sam jako punkt początkowy) i podaj poświadczenia, hello docelowego programu SQL Server.  

   ![Importowanie bazy danych](./media/sql-database-import/import.png)

postęp hello toomonitor hello operacji importu, otwórz stronę hello powitania serwera logicznego zawierającego hello bazy danych zostały zaimportowane. Przewiń w dół za**operacji** , a następnie kliknij przycisk **importu/eksportu** historii.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Monitoruj postęp hello operacji importu

postęp hello toomonitor hello operacji importu, otwórz stronę hello powitania serwera logicznego do których hello bazy danych jest importowany zaimportowane. Przewiń w dół za**operacji** , a następnie kliknij przycisk **importu/eksportu** historii.
   
   ![Importuj](./media/sql-database-import/import-history.png) ![stan importowania](./media/sql-database-import/import-status.png)

Baza danych hello tooverify znajduje się na żywo na powitania serwera, kliknij przycisk **baz danych programu SQL** i sprawdź hello nowej bazy danych jest **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importuj z pliku pliku BACPAC przy użyciu SQLPackage

tooimport SQL bazy danych przy użyciu hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) narzędzie wiersza polecenia, zobacz [zaimportować parametrów i właściwości](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Narzędzie SQLPackage Hello jest dostarczany z hello najnowsze wersje [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) i [programu SQL Server Data Tools dla programu Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), lub hello najnowszą wersję można pobrać [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) bezpośrednio z hello Microsoft Centrum pobierania.

Firma Microsoft zaleca użycie hello hello narzędzie SQLPackage na skalowalność i wydajność w większości środowisk produkcyjnych. Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Zobacz hello następujące polecenia SQLPackage, na przykład skryptu, jak tooimport hello **AdventureWorks2008R2** bazy danych z magazynu lokalnego tooan bazy danych SQL Azure serwer logiczny, nazywany **mynewserver20170403** w tym przykładzie. Ten skrypt pokazuje hello Tworzenie nowej bazy danych o nazwie **myMigratedDatabase**, z warstwy usług z **Premium**, a celem usługi **P6**. Zmień wartości tych jako odpowiednie tooyour środowiska.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![Importuj sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Serwer logiczny usługi Azure SQL Database nasłuchuje na porcie 1433. Jeśli próbujesz tooconnect tooan bazy danych SQL Azure serwera logicznego od w obrębie firmowej zapory, ten port musi być otwarty w hello firmowej zapory dla toosuccessfully można połączyć z usługą.
>

W tym przykładzie pokazano sposób tooimport a bazą danych przy użyciu SqlPackage.exe z uniwersalnych uwierzytelnianie usługi Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importuj z pliku pliku BACPAC przy użyciu programu PowerShell

Użyj hello [AzureRmSqlDatabaseImport nowy](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) toosubmit polecenia cmdlet toohello żądanie importu bazy danych usługi baza danych SQL Azure. W zależności od wielkości hello bazy danych hello operacji importowania może potrwać niektórych toocomplete czasu.

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

Stan hello toocheck hello żądania importowania, użyj hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) polecenia cmdlet. Uruchomiona natychmiast po hello żądania zwykle zwraca **stan: w toku**. Po wyświetleniu **stanu: zakończyło się pomyślnie** hello Importowanie zostało zakończone.

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
Na przykład innego skryptu, zobacz [zaimportować bazę danych z pliku pliku BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Następne kroki
* toolearn tooconnect tooand zapytania importowanych bazy danych SQL, zobacz [uzyskuj tooSQL bazy danych programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md).
* Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Omówienie hello całego programu SQL Server bazy danych procesu migracji, w tym zalecenia dotyczące wydajności, zobacz [migracji tooAzure bazy danych programu SQL Server, bazy danych SQL](sql-database-cloud-migrate.md).



