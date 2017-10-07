---
title: aaaExport pliku pliku BACPAC tooa bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: "Wyeksportuj plik pliku BACPAC tooa bazy danych Azure SQL przy użyciu hello portalu Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Eksportowanie pliku pliku BACPAC tooa bazy danych Azure SQL

Jeśli potrzebujesz tooexport bazy danych do archiwizacji lub przenoszenie tooanother platformy, można wyeksportować hello bazy danych: schemat i dane tooa [pliku BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) pliku. Plik pliku BACPAC to plik ZIP z rozszerzeniem pliku BACPAC zawierające hello metadane i dane z bazy danych programu SQL Server. Plik pliku BACPAC można przechowywanych w magazynie obiektów blob platformy Azure lub w magazynie lokalnym w lokalizacji lokalnej i później zaimportować do bazy danych SQL Azure lub do instalacji lokalnej programu SQL Server. 

> [!IMPORTANT] 
> Azure bazy danych zautomatyzowanego eksportu danych SQL została wycofana w 1 marca 2017 r. Można użyć [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md
) lub [usługi Automatyzacja Azure](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically archiwum baz danych przy użyciu programu PowerShell, zgodnie z harmonogramu tooa wybranych przez użytkownika. Dla przykładu, Pobierz hello [przykładowy skrypt programu PowerShell](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) z usługi Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Zagadnienia dotyczące podczas eksportowania bazy danych Azure SQL

* Eksportu są eksportowane toobe spójna transakcyjnie, należy upewnić się, że nie działania zapisu ma miejsce podczas eksportowania hello, albo że możesz [spójna transakcyjnie kopiowania](sql-database-copy.md) bazy danych Azure SQL.
* Jeśli eksportujesz magazynu tooblob hello maksymalny rozmiar pliku pliku BACPAC jest 200 GB. rozmiar pliku pliku BACPAC tooarchive wyeksportować toolocal magazynu.
* Eksportowanie pliku BACPAC tooAzure premium magazyn plików przy użyciu metod hello omówionych w tym artykule nie jest obsługiwane.
* Jeśli operacja eksportu hello z bazy danych SQL Azure przekracza 20 godzin, mogą zostać anulowane. wydajność tooincrease podczas eksportu, można:
  * Tymczasowo zwiększyć poziom obsługi.
  * Zaprzestanie wszystkie odczytu i zapisu działania podczas eksportowania hello.
  * Użyj [indeksu klastrowanego](https://msdn.microsoft.com/library/ms190457.aspx) o wartości innej niż null na wszystkich dużych tabel. Bez indeksy klastrowane eksportu może nie powieść, jeśli trwa dłużej niż 6 – 12 godzin. Jest to spowodowane hello eksportu usługa musi toocomplete skanowania tootry tooexport całej tabeli. Toodetermine dobrze, jeśli tabele są optymalizowane dla eksportu jest toorun **DBCC SHOW_STATISTICS** i upewnij się, że hello *RANGE_HI_KEY* nie ma wartości null, a jego wartość ma dobrej dystrybucji. Aby uzyskać więcej informacji, zobacz [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> BACPACs nie są zamierzone toobe używane dla operacji tworzenia kopii zapasowej i przywracania. Baza danych SQL Azure automatycznie tworzy kopie zapasowe dla każdej bazy danych użytkownika. Aby uzyskać więcej informacji, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md) i [kopie zapasowe bazy danych SQL](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Eksportowanie pliku pliku BACPAC tooa przy użyciu hello portalu Azure

Witaj tooexport bazy danych przy użyciu [portalu Azure](https://portal.azure.com), otwórz stronę hello bazy danych i kliknij przycisk **wyeksportować** na powitania narzędzi. Określ nazwę pliku BACPAC hello, podaj hello konto magazynu Azure i kontener eksportu hello i podaj hello poświadczenia tooconnect toohello źródłowej bazy danych.  

![Eksportowanie bazy danych](./media/sql-database-export/database-export.png)

postęp hello toomonitor hello operacji eksportowania, otwórz stronę hello powitania serwera logicznego zawierającego hello bazę danych eksportowane. Przewiń w dół za**operacji** , a następnie kliknij przycisk **importu/eksportu** historii.

![Eksportuj historii](./media/sql-database-export/export-history.png)
![stan historii eksportu](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Eksportuj plik pliku BACPAC tooa przy użyciu narzędzia SQLPackage hello

tooexport SQL bazy danych przy użyciu hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) narzędzie wiersza polecenia, zobacz [wyeksportować parametrów i właściwości](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Narzędzie SQLPackage Hello jest dostarczany z hello najnowsze wersje [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) i [programu SQL Server Data Tools dla programu Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), lub hello najnowszą wersję można pobrać [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) bezpośrednio z hello Microsoft Centrum pobierania.

Firma Microsoft zaleca użycie hello hello narzędzie SQLPackage na skalowalność i wydajność w większości środowisk produkcyjnych. Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

W tym przykładzie pokazano sposób tooexport a bazą danych przy użyciu SqlPackage.exe z uniwersalnych uwierzytelnianie usługi Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Eksportuj plik pliku BACPAC tooa przy użyciu programu SQL Server Management Studio (SSMS)

Witaj najnowsza wersja programu SQL Server Management Studio udostępniają tooexport kreatora pliku pliku BACPAC tooa bazy danych SQL Azure. Zobacz hello [eksportowania aplikacji warstwy danych](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Eksportuj plik pliku BACPAC tooa przy użyciu programu PowerShell

Użyj hello [AzureRmSqlDatabaseExport nowy](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) toosubmit polecenia cmdlet toohello żądanie eksportu bazy danych usługi baza danych SQL Azure. W zależności od wielkości hello bazy danych hello eksportu operacja może potrwać kilka toocomplete czas.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

Stan hello toocheck hello żądania eksportu, użyj hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) polecenia cmdlet. Uruchomiona natychmiast po hello żądania zwykle zwraca **stan: w toku**. Po wyświetleniu **stanu: zakończyło się pomyślnie** hello eksportu została ukończona.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Następne kroki

* Zobacz toolearn o długoterminowego przechowywania kopii zapasowych kopii zapasowej bazy danych Azure SQL jako alternatywne tooexported bazy danych do celów archiwum [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md).
- Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Zobacz toolearn Importowanie bazy danych programu SQL Server tooa pliku BACPAC, [Importowanie bazy danych programu SQL Server tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn o Eksportowanie pliku BACPAC bazy danych programu SQL Server, zobacz [eksportowania aplikacji warstwy danych](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) i [migracji pierwszą bazę danych](sql-database-migrate-your-sql-server-database.md).
* Jeśli są eksportowane z programu SQL Server jako tooAzure toomigration prelude bazy danych SQL, zobacz [migracji tooAzure bazy danych programu SQL Server, bazy danych SQL](sql-database-cloud-migrate.md).
