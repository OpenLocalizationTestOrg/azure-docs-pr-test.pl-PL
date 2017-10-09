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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="a0f87-103">Przenoszenie danych tooSQL serwera na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0f87-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="a0f87-104">W tym temacie opisano opcje hello do przenoszenia danych z plików prostych (w formatach CSV lub TSV) lub z lokalnymi tooSQL serwera SQL Server na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f87-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="a0f87-105">Te zadania dla ruchu danych w chmurze toohello są częścią hello proces nauki danych zespołu.</span><span class="sxs-lookup"><span data-stu-id="a0f87-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="a0f87-106">Dla tematu, który zawiera opcje hello do przenoszenia danych tooan bazy danych SQL Azure Machine Learning, zobacz [Przenieś tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a0f87-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="a0f87-107">Witaj **menu** poniżej tootopics łącza, które opisują sposób tooingest danych w innych środowiskach docelowych, gdzie hello dane mogą być przechowywane i przetwarzane podczas hello zespołu danych nauki procesu (TDSP).</span><span class="sxs-lookup"><span data-stu-id="a0f87-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="a0f87-108">Witaj Poniższa tabela zawiera podsumowanie hello Opcje przenoszenia danych tooSQL serwera na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f87-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="a0f87-109"><b>ŹRÓDŁO</b></span><span class="sxs-lookup"><span data-stu-id="a0f87-109"><b>SOURCE</b></span></span> | <span data-ttu-id="a0f87-110"><b>Miejsce docelowe: SQL Server na maszynie Wirtualnej platformy Azure</b></span><span class="sxs-lookup"><span data-stu-id="a0f87-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="a0f87-111"><b>Plik prosty</b></span><span class="sxs-lookup"><span data-stu-id="a0f87-111"><b>Flat File</b></span></span> |<span data-ttu-id="a0f87-112">1. <a href="#insert-tables-bcp">Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="a0f87-113">2. <a href="#insert-tables-bulkquery">Zapytanie SQL wstawiania zbiorczego</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="a0f87-114">3. <a href="#sql-builtin-utilities">Graficznych narzędzi wbudowanych w programie SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="a0f87-115"><b>Lokalny serwer SQL</b></span><span class="sxs-lookup"><span data-stu-id="a0f87-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="a0f87-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Wdrażanie Kreatora bazy danych SQL Server tooa maszyny Wirtualnej programu Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="a0f87-117">2. <a href="#export-flat-file">Eksportuj tooa płaskim pliku</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="a0f87-118">3. <a href="#sql-migration">Kreator migracji bazy danych SQL</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="a0f87-119">4. <a href="#sql-backup">Baza danych kopii zapasowej i przywracanie</a></span><span class="sxs-lookup"><span data-stu-id="a0f87-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="a0f87-120">Pamiętaj, że w tym dokumencie przyjęto założenie, że polecenia SQL są wykonywane z programu SQL Server Management Studio lub Visual Studio Explorer bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a0f87-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="a0f87-121">Alternatywnie, można użyć [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) toocreate i Zaplanuj potok, który zostanie przesunięty tooa danych maszyny Wirtualnej programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f87-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="a0f87-122">Aby uzyskać więcej informacji, zobacz [skopiować dane z fabryką danych Azure (działanie kopiowania)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a0f87-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="a0f87-123"><a name="prereqs"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a0f87-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="a0f87-124">Ten samouczek zakłada, że masz:</span><span class="sxs-lookup"><span data-stu-id="a0f87-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="a0f87-125">**Subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="a0f87-125">An **Azure subscription**.</span></span> <span data-ttu-id="a0f87-126">Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0f87-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a0f87-127">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="a0f87-127">An **Azure storage account**.</span></span> <span data-ttu-id="a0f87-128">Korzystasz z konta magazynu Azure do przechowywania danych hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="a0f87-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="a0f87-129">Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a0f87-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="a0f87-130">Po utworzeniu konta magazynu hello, musisz mieć konto hello tooobtain się, że klucz używany tooaccess hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="a0f87-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="a0f87-131">Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="a0f87-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="a0f87-132">Zainicjowano obsługę administracyjną **programu SQL Server na maszynie Wirtualnej platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="a0f87-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="a0f87-133">Aby uzyskać instrukcje, zobacz [Konfigurowanie maszyny wirtualnej Azure SQL Server jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="a0f87-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="a0f87-134">Zainstalowano i skonfigurowano **programu Azure PowerShell** lokalnie.</span><span class="sxs-lookup"><span data-stu-id="a0f87-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="a0f87-135">Aby uzyskać instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0f87-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="a0f87-136"><a name="filesource_to_sqlonazurevm"></a>Przenoszenie danych z pliku prostego tooSQL źródłowego serwera na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0f87-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="a0f87-137">Dane pochodzą z pliku prostego (ułożone w formacie wierszy i kolumn), może być przeniesiony tooSQL maszyny Wirtualnej serwera na platformie Azure za pośrednictwem hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="a0f87-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="a0f87-138">Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</span><span class="sxs-lookup"><span data-stu-id="a0f87-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="a0f87-139">Zapytanie SQL wstawiania zbiorczego</span><span class="sxs-lookup"><span data-stu-id="a0f87-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="a0f87-140">Graficznych narzędzi wbudowanych w programie SQL Server (importu/eksportu, SSIS)</span><span class="sxs-lookup"><span data-stu-id="a0f87-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="a0f87-141"><a name="insert-tables-bcp"></a>Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</span><span class="sxs-lookup"><span data-stu-id="a0f87-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="a0f87-142">Narzędzie BCP to narzędzie wiersza polecenia zainstalowane z programem SQL Server i jest jednym z hello najszybszy sposób toomove danych.</span><span class="sxs-lookup"><span data-stu-id="a0f87-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="a0f87-143">Działa ona za pośrednictwem wszystkich trzech wariantów programu SQL Server (lokalnego programu SQL Server, SQL Azure i maszyna wirtualna serwera SQL na platformie Azure).</span><span class="sxs-lookup"><span data-stu-id="a0f87-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="a0f87-144">**Gdzie powinien mieć BCP danych?**</span><span class="sxs-lookup"><span data-stu-id="a0f87-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="a0f87-145">Mimo że nie jest wymagany, o plików zawierających źródła danych znajdujących się na powitania, w tym samym komputerze co hello docelowego programu SQL Server umożliwia szybsze transferu (sieci szybkości vs dysku lokalnym szybkości operacji We/Wy).</span><span class="sxs-lookup"><span data-stu-id="a0f87-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="a0f87-146">Można przenieść hello płaskiej pliki zawierające maszyny toohello danych w przypadku, gdy jest zainstalowany program SQL Server przy użyciu różnych kopiowanie plików narzędzi takich jak [AZCopy](../storage/common/storage-use-azcopy.md), [Eksploratora usługi Storage Azure](http://storageexplorer.com/) lub windows kopiowania/wklejania za pomocą zdalnego Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="a0f87-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="a0f87-147">Upewnij się, że hello bazy danych i tabele hello są tworzone w bazie danych programu SQL Server docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="a0f87-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="a0f87-148">Poniżej przedstawiono przykładowy sposób toodo tego za pomocą hello `Create Database` i `Create Table` polecenia:</span><span class="sxs-lookup"><span data-stu-id="a0f87-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="a0f87-149">Generowanie hello format pliku, który opisuje hello schemat tabeli hello wysyłając hello następujące polecenie z wiersza polecenia maszyny hello hello zainstalowanym bcp.</span><span class="sxs-lookup"><span data-stu-id="a0f87-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="a0f87-150">Wstawianie danych hello w hello bazy danych przy użyciu polecenia bcp hello w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="a0f87-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="a0f87-151">Powinno to działać z wiersza polecenia hello przy założeniu, że hello programu SQL Server jest zainstalowany na tym samym komputerze:</span><span class="sxs-lookup"><span data-stu-id="a0f87-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="a0f87-152">**Optymalizacja wstawia BCP** można znaleźć hello poniższego artykułu ["Wytyczne dotyczące importowania zbiorczego optymalizacji"](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) wstawia toooptimize takie.</span><span class="sxs-lookup"><span data-stu-id="a0f87-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="a0f87-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing wstawia dla szybsze przepływu danych</span><span class="sxs-lookup"><span data-stu-id="a0f87-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="a0f87-154">Jeśli przenosisz dane hello jest duży, można przyspieszyć rzeczy, wykonując jednocześnie wiele polecenia BCP równolegle w skrypcie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0f87-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="a0f87-155">**Wprowadzanie danych big data** tabel logicznej i fizycznej bazy danych przy użyciu wielu grup plików i partycji tabeli partycji danych toooptimize ładowania dla dużych i bardzo dużych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="a0f87-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="a0f87-156">Aby uzyskać więcej informacji na temat tworzenia i ładowanie tabel toopartition danych zobacz [równoległych tabel partycji SQL obciążenia](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="a0f87-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="a0f87-157">Witaj Poniższy przykładowy skrypt programu PowerShell pokazują równoległych wstawia przy użyciu narzędzia bcp:</span><span class="sxs-lookup"><span data-stu-id="a0f87-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

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


### <span data-ttu-id="a0f87-158"><a name="insert-tables-bulkquery"></a>Zapytanie SQL wstawiania zbiorczego</span><span class="sxs-lookup"><span data-stu-id="a0f87-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="a0f87-159">[Zbiorcze Wstawianie zapytania SQL](https://msdn.microsoft.com/library/ms188365) mogą być używane tooimport danych hello z do bazy danych plików na podstawie wiersza/kolumny (hello obsługiwane typy są objęte[przygotować dane zbiorcze eksportu lub importu (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tematu.</span><span class="sxs-lookup"><span data-stu-id="a0f87-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="a0f87-160">Poniżej przedstawiono niektóre przykładowe polecenia dla Bulk Insert czy, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="a0f87-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="a0f87-161">Analizowanie danych i niestandardowych opcji przed zaimportowaniem toomake się, że hello takiego samego formatu pól specjalnych, takich jak daty przyjęto założenie, że baza danych programu SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="a0f87-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="a0f87-162">Poniżej przedstawiono przykład sposobu tooset hello datę w formacie rok, miesiąc, dzień (Jeśli dane zawierają hello datę w formacie rok, miesiąc, dzień):</span><span class="sxs-lookup"><span data-stu-id="a0f87-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="a0f87-163">Importowanie danych przy użyciu zbiorczego instrukcje importu:</span><span class="sxs-lookup"><span data-stu-id="a0f87-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="a0f87-164"><a name="sql-builtin-utilities"></a>Wbudowane narzędzia w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="a0f87-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="a0f87-165">Do maszyny Wirtualnej serwera SQL na platformie Azure z pliku prostego, można użyć danych tooimport SQL Server integracji Services (SSIS).</span><span class="sxs-lookup"><span data-stu-id="a0f87-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="a0f87-166">SSIS jest dostępny w dwóch środowisk studio.</span><span class="sxs-lookup"><span data-stu-id="a0f87-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="a0f87-167">Aby uzyskać więcej informacji, zobacz [Integration Services (SSIS) oraz środowisk Studio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="a0f87-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="a0f87-168">Szczegółowe informacje dotyczące programu SQL Server Data Tools, zobacz [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="a0f87-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="a0f87-169">Aby uzyskać szczegółowe informacje na powitania Kreatora importu/eksportu, zobacz [Kreatora programu SQL Server importowania i eksportowania](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="a0f87-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="a0f87-170"><a name="sqlonprem_to_sqlonazurevm"></a>Przenoszenie danych z lokalnego tooSQL serwera SQL Server na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0f87-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="a0f87-171">Można także użyć następujących strategii migracji hello:</span><span class="sxs-lookup"><span data-stu-id="a0f87-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="a0f87-172">Wdrażanie Kreatora bazy danych SQL Server tooa maszyny Wirtualnej programu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a0f87-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="a0f87-173">TooFlat eksportu pliku</span><span class="sxs-lookup"><span data-stu-id="a0f87-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="a0f87-174">Kreator migracji bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="a0f87-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="a0f87-175">Baza danych kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="a0f87-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="a0f87-176">Opisano każdy z tych poniżej:</span><span class="sxs-lookup"><span data-stu-id="a0f87-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="a0f87-177">Wdrażanie Kreatora bazy danych SQL Server tooa maszyny Wirtualnej programu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a0f87-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="a0f87-178">Witaj **wdrażanie Kreatora bazy danych serwera SQL Microsoft Azure VM tooa** dane toomove prosty i zalecany sposób z tooSQL wystąpienia programu SQL Server lokalnego serwera na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f87-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="a0f87-179">Aby uzyskać szczegółowy opis kroków, jak również zapoznać się z omówieniem alternatywnych, zobacz [migracji tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a0f87-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="a0f87-180"><a name="export-flat-file"></a>TooFlat eksportu pliku</span><span class="sxs-lookup"><span data-stu-id="a0f87-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="a0f87-181">Różne metody mogą być używane toobulk eksportowania danych z lokalnego programu SQL Server, zgodnie z opisem w hello [zbiorczego importowanie i eksportowanie danych (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="a0f87-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="a0f87-182">Ten dokument obejmuje hello Program kopiowania zbiorczego (BCP) jako przykład.</span><span class="sxs-lookup"><span data-stu-id="a0f87-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="a0f87-183">Gdy dane są eksportowane do pliku prostego, może być importowany tooanother programu SQL server za pomocą importowania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a0f87-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="a0f87-184">Eksportowanie danych hello z lokalnego programu SQL Server tooa pliku przy użyciu narzędzia bcp hello w następujący sposób</span><span class="sxs-lookup"><span data-stu-id="a0f87-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="a0f87-185">Tworzenie hello bazy danych i tabeli hello na maszynie Wirtualnej serwera SQL na platformie Azure przy użyciu hello `create database` i `create table` dla schematu tabeli hello wyeksportowany w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="a0f87-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="a0f87-186">Tworzenie pliku formatu do opisywania hello schemat tabeli danych hello jest eksportu/importu.</span><span class="sxs-lookup"><span data-stu-id="a0f87-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="a0f87-187">Szczegóły pliku formatu hello są opisane w [Utwórz plik formatu (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0f87-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="a0f87-188">Generowanie pliku formatu podczas uruchamiania narzędzia BCP z hello komputera programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="a0f87-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="a0f87-189">Generowanie pliku formatu podczas uruchamiania narzędzia BCP zdalnie na serwerze SQL</span><span class="sxs-lookup"><span data-stu-id="a0f87-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="a0f87-190">Użyj jednej z metod hello opisane w sekcji [przenoszenia danych z pliku źródłowego](#filesource_to_sqlonazurevm) toomove hello danych plików prostych tooa programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a0f87-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="a0f87-191"><a name="sql-migration"></a>Kreator migracji bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="a0f87-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="a0f87-192">[Kreator migracji bazy danych programu SQL Server](http://sqlazuremw.codeplex.com/) zapewnia toomove przyjazną dla użytkownika sposób dane między dwa wystąpienia programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="a0f87-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="a0f87-193">Umożliwia hello użytkownika toomap hello schemat danych między źródłami a tabel docelowych, wybierz typy kolumn i różnych innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="a0f87-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="a0f87-194">W obszarze obejmuje hello jest używany kopiowania zbiorczego (BCP).</span><span class="sxs-lookup"><span data-stu-id="a0f87-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="a0f87-195">Zrzut ekranu przedstawiający hello Zapraszamy ekranie powitania migracji bazy danych SQL kreatora są wyświetlane poniżej.</span><span class="sxs-lookup"><span data-stu-id="a0f87-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Kreator migracji programu SQL Server][2]

### <span data-ttu-id="a0f87-197"><a name="sql-backup"></a>Baza danych kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="a0f87-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="a0f87-198">SQL Server obsługuje:</span><span class="sxs-lookup"><span data-stu-id="a0f87-198">SQL Server supports:</span></span>

1. <span data-ttu-id="a0f87-199">[Baza danych kopii zapasowej i przywrócenia jej funkcjonalności](https://msdn.microsoft.com/library/ms187048.aspx) (zarówno tooa lokalnego pliku lub pliku bacpac eksportu tooblob) i [aplikacji warstwy danych](https://msdn.microsoft.com/library/ee210546.aspx) (przy użyciu pliku bacpac).</span><span class="sxs-lookup"><span data-stu-id="a0f87-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="a0f87-200">Możliwości toodirectly Tworzenie maszyn wirtualnych programu SQL Server na platformie Azure za pomocą skopiowanego bazy danych lub kopiowania tooan istniejącej bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f87-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="a0f87-201">Aby uzyskać więcej informacji, zobacz [hello Użyj Kreatora kopiowania bazy danych](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0f87-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="a0f87-202">Zrzut ekranu przedstawiający hello kopii bazy danych w górę/przywracania z programu SQL Server Management Studio opcje są wyświetlane poniżej.</span><span class="sxs-lookup"><span data-stu-id="a0f87-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Narzędzie importu programu SQL Server][1]

## <a name="resources"></a><span data-ttu-id="a0f87-204">Zasoby</span><span class="sxs-lookup"><span data-stu-id="a0f87-204">Resources</span></span>
[<span data-ttu-id="a0f87-205">Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0f87-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="a0f87-206">Omówienie programu SQL Server w usłudze Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="a0f87-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
