---
title: aaaMove danych tooSQL serwera na maszynie wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Przenoszenie danych z plików prostych lub lokalnymi tooSQL serwera SQL Server na maszynie Wirtualnej Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Przenoszenie danych tooSQL serwera na maszynie wirtualnej platformy Azure
W tym temacie opisano opcje hello do przenoszenia danych z plików prostych (w formatach CSV lub TSV) lub z lokalnymi tooSQL serwera SQL Server na maszynie wirtualnej platformy Azure. Te zadania dla ruchu danych w chmurze toohello są częścią hello proces nauki danych zespołu.

Dla tematu, który zawiera opcje hello do przenoszenia danych tooan bazy danych SQL Azure Machine Learning, zobacz [Przenieś tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

Witaj **menu** poniżej tootopics łącza, które opisują sposób tooingest danych w innych środowiskach docelowych, gdzie hello dane mogą być przechowywane i przetwarzane podczas hello zespołu danych nauki procesu (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Witaj Poniższa tabela zawiera podsumowanie hello Opcje przenoszenia danych tooSQL serwera na maszynie wirtualnej platformy Azure.

| <b>ŹRÓDŁO</b> | <b>Miejsce docelowe: SQL Server na maszynie Wirtualnej platformy Azure</b> |
| --- | --- |
| <b>Plik prosty</b> |1. <a href="#insert-tables-bcp">Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</a><br> 2. <a href="#insert-tables-bulkquery">Zapytanie SQL wstawiania zbiorczego</a><br> 3. <a href="#sql-builtin-utilities">Graficznych narzędzi wbudowanych w programie SQL Server</a> |
| <b>Lokalny serwer SQL</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Wdrażanie Kreatora bazy danych SQL Server tooa maszyny Wirtualnej programu Microsoft Azure</a><br> 2. <a href="#export-flat-file">Eksportuj tooa płaskim pliku</a><br> 3. <a href="#sql-migration">Kreator migracji bazy danych SQL</a> <br> 4. <a href="#sql-backup">Baza danych kopii zapasowej i przywracanie</a><br> |

Pamiętaj, że w tym dokumencie przyjęto założenie, że polecenia SQL są wykonywane z programu SQL Server Management Studio lub Visual Studio Explorer bazy danych.

> [!TIP]
> Alternatywnie, można użyć [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) toocreate i Zaplanuj potok, który zostanie przesunięty tooa danych maszyny Wirtualnej programu SQL Server na platformie Azure. Aby uzyskać więcej informacji, zobacz [skopiować dane z fabryką danych Azure (działanie kopiowania)](../data-factory/data-factory-data-movement-activities.md).
>
>

## <a name="prereqs"></a>Wymagania wstępne
Ten samouczek zakłada, że masz:

* **Subskrypcji platformy Azure**. Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* **Konto magazynu Azure**. Korzystasz z konta magazynu Azure do przechowywania danych hello w tym samouczku. Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu. Po utworzeniu konta magazynu hello, musisz mieć konto hello tooobtain się, że klucz używany tooaccess hello magazynu. Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Zainicjowano obsługę administracyjną **programu SQL Server na maszynie Wirtualnej platformy Azure**. Aby uzyskać instrukcje, zobacz [Konfigurowanie maszyny wirtualnej Azure SQL Server jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* Zainstalowano i skonfigurowano **programu Azure PowerShell** lokalnie. Aby uzyskać instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Przenoszenie danych z pliku prostego tooSQL źródłowego serwera na maszynie Wirtualnej platformy Azure
Dane pochodzą z pliku prostego (ułożone w formacie wierszy i kolumn), może być przeniesiony tooSQL maszyny Wirtualnej serwera na platformie Azure za pośrednictwem hello następujące metody:

1. [Narzędzie Kopia wiersza polecenia zbiorczego (BCP)](#insert-tables-bcp)
2. [Zapytanie SQL wstawiania zbiorczego](#insert-tables-bulkquery)
3. [Graficznych narzędzi wbudowanych w programie SQL Server (importu/eksportu, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Narzędzie Kopia wiersza polecenia zbiorczego (BCP)
Narzędzie BCP to narzędzie wiersza polecenia zainstalowane z programem SQL Server i jest jednym z hello najszybszy sposób toomove danych. Działa ona za pośrednictwem wszystkich trzech wariantów programu SQL Server (lokalnego programu SQL Server, SQL Azure i maszyna wirtualna serwera SQL na platformie Azure).

> [!NOTE]
> **Gdzie powinien mieć BCP danych?**  
> Mimo że nie jest wymagany, o plików zawierających źródła danych znajdujących się na powitania, w tym samym komputerze co hello docelowego programu SQL Server umożliwia szybsze transferu (sieci szybkości vs dysku lokalnym szybkości operacji We/Wy). Można przenieść hello płaskiej pliki zawierające maszyny toohello danych w przypadku, gdy jest zainstalowany program SQL Server przy użyciu różnych kopiowanie plików narzędzi takich jak [AZCopy](../storage/common/storage-use-azcopy.md), [Eksploratora usługi Storage Azure](http://storageexplorer.com/) lub windows kopiowania/wklejania za pomocą zdalnego Desktop Protocol (RDP).
>
>

1. Upewnij się, że hello bazy danych i tabele hello są tworzone w bazie danych programu SQL Server docelowym hello. Poniżej przedstawiono przykładowy sposób toodo tego za pomocą hello `Create Database` i `Create Table` polecenia:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Generowanie hello format pliku, który opisuje hello schemat tabeli hello wysyłając hello następujące polecenie z wiersza polecenia maszyny hello hello zainstalowanym bcp.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Wstawianie danych hello w hello bazy danych przy użyciu polecenia bcp hello w następujący sposób. Powinno to działać z wiersza polecenia hello przy założeniu, że hello programu SQL Server jest zainstalowany na tym samym komputerze:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **Optymalizacja wstawia BCP** można znaleźć hello poniższego artykułu ["Wytyczne dotyczące importowania zbiorczego optymalizacji"](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) wstawia toooptimize takie.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Parallelizing wstawia dla szybsze przepływu danych
Jeśli przenosisz dane hello jest duży, można przyspieszyć rzeczy, wykonując jednocześnie wiele polecenia BCP równolegle w skrypcie programu PowerShell.

> [!NOTE]
> **Wprowadzanie danych big data** tabel logicznej i fizycznej bazy danych przy użyciu wielu grup plików i partycji tabeli partycji danych toooptimize ładowania dla dużych i bardzo dużych zestawów danych. Aby uzyskać więcej informacji na temat tworzenia i ładowanie tabel toopartition danych zobacz [równoległych tabel partycji SQL obciążenia](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Witaj Poniższy przykładowy skrypt programu PowerShell pokazują równoległych wstawia przy użyciu narzędzia bcp:

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>Zapytanie SQL wstawiania zbiorczego
[Zbiorcze Wstawianie zapytania SQL](https://msdn.microsoft.com/library/ms188365) mogą być używane tooimport danych hello z do bazy danych plików na podstawie wiersza/kolumny (hello obsługiwane typy są objęte[przygotować dane zbiorcze eksportu lub importu (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tematu.

Poniżej przedstawiono niektóre przykładowe polecenia dla Bulk Insert czy, jak pokazano poniżej:  

1. Analizowanie danych i niestandardowych opcji przed zaimportowaniem toomake się, że hello takiego samego formatu pól specjalnych, takich jak daty przyjęto założenie, że baza danych programu SQL Server hello. Poniżej przedstawiono przykład sposobu tooset hello datę w formacie rok, miesiąc, dzień (Jeśli dane zawierają hello datę w formacie rok, miesiąc, dzień):

        SET DATEFORMAT ymd;    
2. Importowanie danych przy użyciu zbiorczego instrukcje importu:

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Wbudowane narzędzia w programie SQL Server
Do maszyny Wirtualnej serwera SQL na platformie Azure z pliku prostego, można użyć danych tooimport SQL Server integracji Services (SSIS).
SSIS jest dostępny w dwóch środowisk studio. Aby uzyskać więcej informacji, zobacz [Integration Services (SSIS) oraz środowisk Studio](https://technet.microsoft.com/library/ms140028.aspx):

* Szczegółowe informacje dotyczące programu SQL Server Data Tools, zobacz [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)  
* Aby uzyskać szczegółowe informacje na powitania Kreatora importu/eksportu, zobacz [Kreatora programu SQL Server importowania i eksportowania](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Przenoszenie danych z lokalnego tooSQL serwera SQL Server na maszynie Wirtualnej platformy Azure
Można także użyć następujących strategii migracji hello:

1. [Wdrażanie Kreatora bazy danych SQL Server tooa maszyny Wirtualnej programu Microsoft Azure](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [TooFlat eksportu pliku](#export-flat-file)
3. [Kreator migracji bazy danych SQL](#sql-migration)
4. [Baza danych kopii zapasowej i przywracanie](#sql-backup)

Opisano każdy z tych poniżej:

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Wdrażanie Kreatora bazy danych SQL Server tooa maszyny Wirtualnej programu Microsoft Azure
Witaj **wdrażanie Kreatora bazy danych serwera SQL Microsoft Azure VM tooa** dane toomove prosty i zalecany sposób z tooSQL wystąpienia programu SQL Server lokalnego serwera na maszynie Wirtualnej platformy Azure. Aby uzyskać szczegółowy opis kroków, jak również zapoznać się z omówieniem alternatywnych, zobacz [migracji tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>TooFlat eksportu pliku
Różne metody mogą być używane toobulk eksportowania danych z lokalnego programu SQL Server, zgodnie z opisem w hello [zbiorczego importowanie i eksportowanie danych (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tematu. Ten dokument obejmuje hello Program kopiowania zbiorczego (BCP) jako przykład. Gdy dane są eksportowane do pliku prostego, może być importowany tooanother programu SQL server za pomocą importowania zbiorczego.

1. Eksportowanie danych hello z lokalnego programu SQL Server tooa pliku przy użyciu narzędzia bcp hello w następujący sposób

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Tworzenie hello bazy danych i tabeli hello na maszynie Wirtualnej serwera SQL na platformie Azure przy użyciu hello `create database` i `create table` dla schematu tabeli hello wyeksportowany w kroku 1.
3. Tworzenie pliku formatu do opisywania hello schemat tabeli danych hello jest eksportu/importu. Szczegóły pliku formatu hello są opisane w [Utwórz plik formatu (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Generowanie pliku formatu podczas uruchamiania narzędzia BCP z hello komputera programu SQL Server

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Generowanie pliku formatu podczas uruchamiania narzędzia BCP zdalnie na serwerze SQL

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Użyj jednej z metod hello opisane w sekcji [przenoszenia danych z pliku źródłowego](#filesource_to_sqlonazurevm) toomove hello danych plików prostych tooa programu SQL Server.

### <a name="sql-migration"></a>Kreator migracji bazy danych SQL
[Kreator migracji bazy danych programu SQL Server](http://sqlazuremw.codeplex.com/) zapewnia toomove przyjazną dla użytkownika sposób dane między dwa wystąpienia programu SQL server. Umożliwia hello użytkownika toomap hello schemat danych między źródłami a tabel docelowych, wybierz typy kolumn i różnych innych funkcji. W obszarze obejmuje hello jest używany kopiowania zbiorczego (BCP). Zrzut ekranu przedstawiający hello Zapraszamy ekranie powitania migracji bazy danych SQL kreatora są wyświetlane poniżej.  

![Kreator migracji programu SQL Server][2]

### <a name="sql-backup"></a>Baza danych kopii zapasowej i przywracanie
SQL Server obsługuje:

1. [Baza danych kopii zapasowej i przywrócenia jej funkcjonalności](https://msdn.microsoft.com/library/ms187048.aspx) (zarówno tooa lokalnego pliku lub pliku bacpac eksportu tooblob) i [aplikacji warstwy danych](https://msdn.microsoft.com/library/ee210546.aspx) (przy użyciu pliku bacpac).
2. Możliwości toodirectly Tworzenie maszyn wirtualnych programu SQL Server na platformie Azure za pomocą skopiowanego bazy danych lub kopiowania tooan istniejącej bazy danych SQL Azure. Aby uzyskać więcej informacji, zobacz [hello Użyj Kreatora kopiowania bazy danych](https://msdn.microsoft.com/library/ms188664.aspx).

Zrzut ekranu przedstawiający hello kopii bazy danych w górę/przywracania z programu SQL Server Management Studio opcje są wyświetlane poniżej.

![Narzędzie importu programu SQL Server][1]

## <a name="resources"></a>Zasoby
[Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Omówienie programu SQL Server w usłudze Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
