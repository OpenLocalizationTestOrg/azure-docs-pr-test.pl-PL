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
ms.workload: Active
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 34dee9511822acec46ba4854729939b84f3c06c6
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a>Importowanie pliku pliku BACPAC do nowej bazy danych SQL Azure

Kiedy należy zaimportować bazę danych z archiwum lub podczas migracji z innej platformy, można zaimportować schematu bazy danych i danych z [pliku BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) pliku. Plik pliku BACPAC to plik ZIP z rozszerzeniem pliku BACPAC zawierający metadane i dane z bazy danych programu SQL Server. Można zaimportować pliku BACPAC pliku z magazynu obiektów blob platformy Azure (tylko w przypadku magazynu standard) lub z magazynu lokalnego w lokalizacji lokalnej. Aby zmaksymalizować szybkość importu, firma Microsoft zaleca określić wyższej wydajności i warstwę poziomu usługi, takie jak P6, a następnie skalować w dół zgodnie z potrzebami, po pomyślnym zaimportowaniu. Ponadto poziom zgodności bazy danych po zaimportowaniu opiera się na poziom zgodności źródłowej bazy danych. 

> [!IMPORTANT] 
> Po przeprowadzeniu migracji bazy danych do bazy danych SQL Azure, są dostępne do obsługi bazy danych na jego bieżący poziom zgodności (poziom 100 AdventureWorks2008R2 bazy danych) lub na wyższym poziomie. Aby uzyskać więcej informacji na wpływ i opcje dla działania bazy danych na poziomie zgodności określonego, zobacz [zmienić poziom zgodności bazy danych](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Zobacz też [ALTER DATABASE CONFIGURATION zakres](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) informacji o dodatkowe ustawienia bazy danych na poziomie związane z poziomy zgodności.   >

> [!NOTE]
> Aby zaimportować pliku BACPAC do nowej bazy danych, należy najpierw utworzyć serwera logicznego bazy danych SQL Azure. Samouczek pokazuje, jak przeprowadzić migrację bazy danych programu SQL Server z bazą danych SQL Azure przy użyciu SQLPackage, zobacz [migracji bazy danych programu SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importuj z pliku pliku BACPAC przy użyciu portalu Azure

Ten artykuł zawiera wskazówki dotyczące tworzenia bazy danych Azure SQL z pliku pliku BACPAC przechowywane przy użyciu magazynu obiektów blob platformy Azure [portalu Azure](https://portal.azure.com). Importowanie przy użyciu portalu Azure tylko obsługuje importowanie pliku BACPAC plik z magazynu obiektów blob platformy Azure.

Aby zaimportować bazę danych przy użyciu portalu Azure, otwórz stronę dla serwera bazy danych, aby skojarzyć, a następnie kliknij przycisk **zaimportować** na pasku narzędzi. Określ konto magazynu i kontener, a następnie wybierz plik do zaimportowania pliku BACPAC. Wybierz rozmiar nowej bazy danych (zazwyczaj takie same jak pochodzenia) i poświadczenia serwera SQL miejsca docelowego.  

   ![Importowanie bazy danych](./media/sql-database-import/import.png)

Aby monitorować postęp operacji importowania, otwórz stronę dla serwera logicznego zawierającego bazę danych zostały zaimportowane. Przewiń w dół do **operacji** , a następnie kliknij przycisk **importu/eksportu** historii.

### <a name="monitor-the-progress-of-an-import-operation"></a>Monitoruj postęp operacji importowania

Aby monitorować postęp operacji importowania, otwórz stronę logicznego serwera, do którego jest importowany bazy danych zaimportowane. Przewiń w dół do **operacji** , a następnie kliknij przycisk **importu/eksportu** historii.
   
   ![Importuj](./media/sql-database-import/import-history.png) ![stan importowania](./media/sql-database-import/import-status.png)

Aby sprawdzić, baza danych znajduje się na żywo na serwerze, kliknij przycisk **baz danych SQL** i sprawdź nowej bazy danych jest **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importuj z pliku pliku BACPAC przy użyciu SQLPackage

Aby zaimportować bazę danych SQL przy użyciu [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) narzędzie wiersza polecenia, zobacz [zaimportować parametrów i właściwości](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Narzędzie SQLPackage jest dostarczany z najnowszej wersji [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) i [programu SQL Server Data Tools dla programu Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), można również pobrać najnowszą wersję [SqlPackage ](https://www.microsoft.com/download/details.aspx?id=53876) bezpośrednio z Centrum pobierania Microsoft.

Firma Microsoft zaleca użycie narzędzia SQLPackage na skalowalność i wydajność w większości środowisk produkcyjnych. Aby poczytać o migracji za pomocą plików BACPAC na blogu SQL Server Customer Advisory Team, zobacz [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrowanie z programu SQL Server do usługi Azure SQL Database za pomocą plików BACPAC).

Zobacz następujące polecenie SQLPackage na przykład skryptu dla importowanie **AdventureWorks2008R2** bazy danych z magazynu lokalnego do serwera logicznego bazy danych SQL Azure, o nazwie **mynewserver20170403** w tym przykładzie. Ten skrypt pokazuje Tworzenie nowej bazy danych o nazwie **myMigratedDatabase**, z warstwy usług z **Premium**, a celem usługi **P6**. Zmiany tych wartości odpowiednich dla danego środowiska.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

> [!IMPORTANT]
> Serwer logiczny usługi Azure SQL Database nasłuchuje na porcie 1433. Jeśli próbujesz nawiązać połączenie z serwerem logicznym usługi Azure SQL Database za pośrednictwem zapory firmowej, to aby połączenie się powiodło, ten port musi być otwarty w zaporze firmowej.
>

W tym przykładzie pokazano, jak zaimportować bazę danych przy użyciu SqlPackage.exe z uniwersalnych uwierzytelnianie usługi Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importuj z pliku pliku BACPAC przy użyciu programu PowerShell

Użyj [AzureRmSqlDatabaseImport nowy](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) polecenia cmdlet, aby przesłać żądanie importu bazy danych do usługi baza danych SQL Azure. W zależności od rozmiaru bazy danych operacji importowania może potrwać trochę czasu.

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

Aby sprawdzić stan żądania importu, należy użyć [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) polecenia cmdlet. Uruchomiona natychmiast po odebraniu żądania zwykle zwraca **stan: w toku**. Po wyświetleniu **stanu: zakończyło się pomyślnie** Importowanie zostało zakończone.

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
* Aby dowiedzieć się, jak nawiązać połączenie i zapytanie importowanych bazy danych SQL, zobacz [Połącz z bazą danych SQL za pomocą programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md).
* Aby poczytać o migracji za pomocą plików BACPAC na blogu SQL Server Customer Advisory Team, zobacz [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrowanie z programu SQL Server do usługi Azure SQL Database za pomocą plików BACPAC).
* Omówienie całego programu SQL Server bazy danych procesu migracji, w tym zalecenia dotyczące wydajności, zobacz [migrację bazy danych programu SQL Server do bazy danych SQL Azure](sql-database-cloud-migrate.md).



