---
title: "aaaBuild i zoptymalizować tabel fast równoległych importowania danych do programu SQL Server na maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Równoległy zbiorczy import danych przy użyciu tabeli partycji SQL"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Równoległy zbiorczy import danych przy użyciu tabeli partycji SQL
W tym dokumencie opisano, jak toobuild partycjonowane tabele do importowania zbiorczego fast równoległych bazy danych programu SQL Server tooa danych. Dane big data ładowania/transfer tooa bazy danych SQL, importowanie danych toohello bazy danych SQL i kolejne zapytania można zwiększyć za pomocą *partycjonowane tabele i widoki*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Utwórz nową bazę danych i zestaw grup plików
* [Utwórz nową bazę danych](https://technet.microsoft.com/library/ms176061.aspx), jeśli jest ona już nie istnieje.
* Dodawanie grup plików toohello baza danych, które będą przechowywane pliki fizyczne hello podzielona na partycje. Można to zrobić z [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) w przypadku nowego lub [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) Jeśli hello bazy danych już istnieje.
* Dodaj jeden lub więcej plików (w razie potrzeby) tooeach grupie plików bazy danych.
  
  > [!NOTE]
  > Określ hello grupie plików docelowej, która przechowuje dane dla tej partycji i hello nazwy plików fizyczna baza danych przechowywania hello grupy plików danych.
  > 
  > 

Witaj poniższy przykład tworzy nową bazę danych z trzech grup plików niż hello podstawowej i grupy dzienników, zawierających jeden plik fizyczny w każdym. pliki bazy danych Hello są tworzone w hello domyślnym folderem danych programu SQL Server, zgodnie z konfiguracją hello wystąpienia programu SQL Server. Aby uzyskać więcej informacji na temat hello domyślne lokalizacje plików, zobacz [lokalizacje domyślne i nazwane wystąpienia programu SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a>Tworzenie tabeli partycjonowanej
Tworzenie tabel podzielonym na partycje według schematu danych toohello, grup plików bazy danych zamapowanych toohello utworzony w poprzednim kroku hello. Gdy dane są importowane zbiorczego toohello partycjonowane tabele, rekordy będą dystrybuowane między hello grup plików zgodnie z tooa schemat partycji, zgodnie z poniższym opisem.

**toocreate tabeli partycji, musisz:**

* [Utwórz funkcję partycji](https://msdn.microsoft.com/library/ms187802.aspx) definiujący hello zakres wartości/granice toobe zawarte w każdej tabeli poszczególnych partycji, np. partycje toolimit według miesięcy (niektóre\_datetime\_pole) w roku hello 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Tworzenie schematu partycji](https://msdn.microsoft.com/library/ms179854.aspx) każdego zakresu partycji hello partycji funkcja tooa fizycznego grupy plików, który mapuje np.:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  zakresy hello tooverify obowiązywać w każdej partycji zgodnie z toohello funkcji systemu, uruchom następujące zapytanie hello:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Tworzenie tabeli partycjonowanej](https://msdn.microsoft.com/library/ms174979.aspx)(s) zgodnie z tooyour schemat danych, a następnie określ hello partycji schematu i ograniczenie pole używane toopartition hello tabeli, np.:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Aby uzyskać więcej informacji, zobacz [tworzenia tabel na partycje i indeksów](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Zbiorcze importowanie hello danych dla każdej tabeli poszczególnych partycji
* Możesz użyć narzędzia BCP, BULK INSERT lub innych metod takich jak [Kreator migracji programu SQL Server](http://sqlazuremw.codeplex.com/). przykład Witaj podane używa metody BCP hello.
* [Zmiany bazy danych hello](https://msdn.microsoft.com/library/bb522682.aspx) transakcji toochange rejestrowania schemat tooBULK_LOGGED toominimize koszty rejestrowania, np.:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* dane tooexpedite ładowania, uruchom operacji importowania zbiorczego hello równolegle. Aby uzyskać wskazówki dotyczące usprawnienia zbiorczego importowanie danych big data do baz danych programu SQL Server, zobacz [załadować 1TB w mniej niż 1 godzina](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Witaj następujący skrypt programu PowerShell jest przykładem równoległego ładowania, przy użyciu narzędzia BCP danych.

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Tworzenie indeksów toooptimize sprzężenia i wydajność zapytań
* Jeśli dane do modelowania wyodrębni z wielu tabel, utworzyć indeksy na hello sprzężenia klucze tooimprove hello sprzężenia wydajności.
* [Tworzenie indeksów](https://technet.microsoft.com/library/ms188783.aspx) (klastrowanych lub nieklastrowanych) elementów docelowych np. hello tej samej grupy plików dla każdej partycji dla:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  Lub,
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Możesz wybrać toocreate indeksów hello przed importu danych hello zbiorczego. Tworzenie indeksów, przed zaimportowaniem zbiorczego spowolni ładowania danych hello.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Proces zaawansowane metody analizy i technologii w przykładzie akcji
Przykład wskazówki na trasie przy użyciu hello Cortana Analytics procesu z publicznego zestawu danych, zobacz [Cortana Analytics procesu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

