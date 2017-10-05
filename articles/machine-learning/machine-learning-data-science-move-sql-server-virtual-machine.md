---
title: Przenoszenie danych do programu SQL Server na maszynie wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Przenoszenie danych z plików prostych lub z lokalnego programu SQL Server do programu SQL Server na maszynie Wirtualnej Azure."
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="b4d7a-103">Przenoszenie danych do programu SQL Server na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b4d7a-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="b4d7a-104">W tym temacie opisano opcje przenoszenia danych z plików prostych (w formatach CSV lub TSV) lub z lokalnego programu SQL Server do programu SQL Server na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="b4d7a-105">Te zadania przenoszenie danych w chmurze są częścią procesu nauki danych zespołu.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="b4d7a-106">Aby temacie, który zawiera opcje przenoszenia danych do bazy danych SQL Azure dla uczenia maszynowego, zobacz [przenieść dane do bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="b4d7a-107">**Menu** poniżej łącza do tematów opisujących sposób pozyskiwania danych w innych środowiskach docelowych, gdzie dane mogą być przechowywane i przetwarzane podczas procesu nauki danych zespołu (TDSP).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="b4d7a-108">W poniższej tabeli przedstawiono opcje przenoszenia danych do programu SQL Server na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="b4d7a-109"><b>ŹRÓDŁO</b></span><span class="sxs-lookup"><span data-stu-id="b4d7a-109"><b>SOURCE</b></span></span> | <span data-ttu-id="b4d7a-110"><b>Miejsce docelowe: SQL Server na maszynie Wirtualnej platformy Azure</b></span><span class="sxs-lookup"><span data-stu-id="b4d7a-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="b4d7a-111"><b>Plik prosty</b></span><span class="sxs-lookup"><span data-stu-id="b4d7a-111"><b>Flat File</b></span></span> |<span data-ttu-id="b4d7a-112">1. <a href="#insert-tables-bcp">Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="b4d7a-113">2. <a href="#insert-tables-bulkquery">Zapytanie SQL wstawiania zbiorczego</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="b4d7a-114">3. <a href="#sql-builtin-utilities">Graficznych narzędzi wbudowanych w programie SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="b4d7a-115"><b>Lokalny serwer SQL</b></span><span class="sxs-lookup"><span data-stu-id="b4d7a-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="b4d7a-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Wdrażanie bazy danych programu SQL Server do kreatora maszyny Wirtualnej programu Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="b4d7a-117">2. <a href="#export-flat-file">Wyeksportuj do pliku prostego</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="b4d7a-118">3. <a href="#sql-migration">Kreator migracji bazy danych SQL</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="b4d7a-119">4. <a href="#sql-backup">Baza danych kopii zapasowej i przywracanie</a></span><span class="sxs-lookup"><span data-stu-id="b4d7a-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="b4d7a-120">Pamiętaj, że w tym dokumencie przyjęto założenie, że polecenia SQL są wykonywane z programu SQL Server Management Studio lub Visual Studio Explorer bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="b4d7a-121">Alternatywnie, można użyć [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) do tworzenia i planowania potok, który będzie przenoszenie danych do maszyny Wirtualnej z programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="b4d7a-122">Aby uzyskać więcej informacji, zobacz [skopiować dane z fabryką danych Azure (działanie kopiowania)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="b4d7a-123"><a name="prereqs"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b4d7a-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="b4d7a-124">Ten samouczek zakłada, że masz:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="b4d7a-125">**Subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-125">An **Azure subscription**.</span></span> <span data-ttu-id="b4d7a-126">Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b4d7a-127">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-127">An **Azure storage account**.</span></span> <span data-ttu-id="b4d7a-128">Korzystasz z konta magazynu Azure do przechowywania danych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="b4d7a-129">Jeśli nie masz konta magazynu platformy Azure, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="b4d7a-130">Po utworzeniu konta magazynu, należy uzyskać klucz konto umożliwia dostęp do magazynu.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="b4d7a-131">Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="b4d7a-132">Zainicjowano obsługę administracyjną **programu SQL Server na maszynie Wirtualnej platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="b4d7a-133">Aby uzyskać instrukcje, zobacz [Konfigurowanie maszyny wirtualnej Azure SQL Server jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="b4d7a-134">Zainstalowano i skonfigurowano **programu Azure PowerShell** lokalnie.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="b4d7a-135">Aby uzyskać instrukcje, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="b4d7a-136"><a name="filesource_to_sqlonazurevm"></a>Przenoszenie danych ze źródła pliku prostego do programu SQL Server na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b4d7a-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="b4d7a-137">Jeśli dane pliku prostego (ułożone w formacie wierszy i kolumn), można ją przenosić do maszyny Wirtualnej programu SQL Server na platformie Azure za pomocą następujących metod:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="b4d7a-138">Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</span><span class="sxs-lookup"><span data-stu-id="b4d7a-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="b4d7a-139">Zapytanie SQL wstawiania zbiorczego</span><span class="sxs-lookup"><span data-stu-id="b4d7a-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="b4d7a-140">Graficznych narzędzi wbudowanych w programie SQL Server (importu/eksportu, SSIS)</span><span class="sxs-lookup"><span data-stu-id="b4d7a-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="b4d7a-141"><a name="insert-tables-bcp"></a>Narzędzie Kopia wiersza polecenia zbiorczego (BCP)</span><span class="sxs-lookup"><span data-stu-id="b4d7a-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="b4d7a-142">Narzędzie BCP to narzędzie wiersza polecenia zainstalowane z programem SQL Server i jest najszybszym sposoby przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="b4d7a-143">Działa ona za pośrednictwem wszystkich trzech wariantów programu SQL Server (lokalnego programu SQL Server, SQL Azure i maszyna wirtualna serwera SQL na platformie Azure).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="b4d7a-144">**Gdzie powinien mieć BCP danych?**</span><span class="sxs-lookup"><span data-stu-id="b4d7a-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="b4d7a-145">Mimo że nie jest wymagane, o pliki zawierające źródło danych znajdujących się na tym samym komputerze co docelowego programu SQL Server umożliwia szybsze transferu (sieci szybkości vs dysku lokalnym szybkości operacji We/Wy).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="b4d7a-146">Można przenieść plików prostych zawierający dane do komputera w przypadku, gdy jest zainstalowany program SQL Server przy użyciu różnych kopiowanie plików narzędzi takich jak [AZCopy](../storage/common/storage-use-azcopy.md), [Eksploratora usługi Storage Azure](http://storageexplorer.com/) lub windows kopiowania/wklejania za pośrednictwem pulpitu zdalnego Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="b4d7a-147">Upewnij się, że baza danych i tabele są tworzone na docelowej bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="b4d7a-148">Poniżej przedstawiono przykład sposobu wykonania tego za pomocą `Create Database` i `Create Table` polecenia:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="b4d7a-149">Generowanie pliku formatu, który opisuje schematu dla tabeli, wydając polecenie w wierszu polecenia na komputerze zainstalowanym bcp.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="b4d7a-150">Wstawianie danych do bazy danych przy użyciu polecenia bcp w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="b4d7a-151">Powinno to działać z wiersza polecenia, przy założeniu, że serwer SQL jest zainstalowany na tym samym komputerze:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="b4d7a-152">**Optymalizacja wstawia BCP** można znaleźć w artykule ["Wytyczne dotyczące importowania zbiorczego optymalizacji"](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) w celu zoptymalizowania takich operacji wstawienia.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="b4d7a-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing wstawia dla szybsze przepływu danych</span><span class="sxs-lookup"><span data-stu-id="b4d7a-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="b4d7a-154">Jeśli dane, które chcesz przenieść jest duży, można przyspieszyć rzeczy, wykonując jednocześnie wiele polecenia BCP równolegle w skrypcie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d7a-155">**Wprowadzanie danych big data** w celu zoptymalizowania danych ładowania dla dużych i bardzo dużych zestawów danych, partycji tabel logicznej i fizycznej bazy danych przy użyciu wielu grup plików i partycji tabeli.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="b4d7a-156">Aby uzyskać więcej informacji na temat tworzenia i ładowanie danych do tabel partycji, zobacz [równoległych tabel partycji SQL obciążenia](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="b4d7a-157">Poniższy przykładowy skrypt programu PowerShell pokazują równoległych wstawia przy użyciu narzędzia bcp:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="b4d7a-158"><a name="insert-tables-bulkquery"></a>Zapytanie SQL wstawiania zbiorczego</span><span class="sxs-lookup"><span data-stu-id="b4d7a-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="b4d7a-159">[Zbiorcze Wstawianie zapytania SQL](https://msdn.microsoft.com/library/ms188365) może służyć do importowania danych do bazy danych z plików na podstawie wiersza/kolumny (obsługiwane typy są objęte[przygotować dane zbiorcze eksportu lub importu (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tematu.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="b4d7a-160">Poniżej przedstawiono niektóre przykładowe polecenia dla Bulk Insert czy, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="b4d7a-161">Analizowanie danych i niestandardowych opcji przed zaimportowaniem, aby upewnić się, że bazy danych programu SQL Server zakłada ten sam format pól specjalnych, takich jak daty.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="b4d7a-162">Poniżej przedstawiono przykład sposobu ustawiania format daty rok, miesiąc, dzień (Jeśli dane zawierają datę w formacie rok, miesiąc, dzień):</span><span class="sxs-lookup"><span data-stu-id="b4d7a-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="b4d7a-163">Importowanie danych przy użyciu zbiorczego instrukcje importu:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="b4d7a-164"><a name="sql-builtin-utilities"></a>Wbudowane narzędzia w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="b4d7a-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="b4d7a-165">SQL Server integracji Services (SSIS) służy do importowania danych do maszyny Wirtualnej serwera SQL na platformie Azure z pliku prostego.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="b4d7a-166">SSIS jest dostępny w dwóch środowisk studio.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="b4d7a-167">Aby uzyskać więcej informacji, zobacz [Integration Services (SSIS) oraz środowisk Studio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="b4d7a-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="b4d7a-168">Szczegółowe informacje dotyczące programu SQL Server Data Tools, zobacz [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="b4d7a-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="b4d7a-169">Aby uzyskać więcej informacji o Kreatorze importu/eksportu, zobacz [Kreatora programu SQL Server importowania i eksportowania](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="b4d7a-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="b4d7a-170"><a name="sqlonprem_to_sqlonazurevm"></a>Przenoszenie danych z lokalnego programu SQL Server do programu SQL Server na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b4d7a-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="b4d7a-171">Można także użyć następujących strategii migracji:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="b4d7a-172">Wdrażanie bazy danych programu SQL Server do kreatora maszyny Wirtualnej programu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b4d7a-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="b4d7a-173">Wyeksportuj do pliku prostego</span><span class="sxs-lookup"><span data-stu-id="b4d7a-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="b4d7a-174">Kreator migracji bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b4d7a-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="b4d7a-175">Baza danych kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="b4d7a-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="b4d7a-176">Opisano każdy z tych poniżej:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="b4d7a-177">Wdrażanie bazy danych programu SQL Server do kreatora maszyny Wirtualnej programu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b4d7a-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="b4d7a-178">**Wdrażania bazy danych programu SQL Server do kreatora Microsoft Azure VM** jest proste i zalecanym sposobem przenoszenia danych z lokalnego wystąpienia programu SQL Server do programu SQL Server na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="b4d7a-179">Aby uzyskać szczegółowy opis kroków, jak również zapoznać się z omówieniem alternatywnych, zobacz [migrację bazy danych do programu SQL Server na maszynie Wirtualnej platformy Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="b4d7a-180"><a name="export-flat-file"></a>Wyeksportuj do pliku prostego</span><span class="sxs-lookup"><span data-stu-id="b4d7a-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="b4d7a-181">Różne metody może służyć do zbiorczego eksportowania danych z lokalnego programu SQL Server, zgodnie z opisem w [zbiorczego importowanie i eksportowanie danych (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="b4d7a-182">Ten dokument obejmują na przykład Program kopiowania zbiorczego (BCP).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="b4d7a-183">Gdy dane są eksportowane do pliku prostego, można je zaimportować do innego serwera SQL za pomocą importowania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="b4d7a-184">Eksportowanie danych z lokalnego serwera SQL w pliku za pomocą narzędzia bcp w następujący sposób</span><span class="sxs-lookup"><span data-stu-id="b4d7a-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="b4d7a-185">Tworzenie bazy danych i tabeli na maszynie Wirtualnej programu SQL Server przy użyciu usługi Azure `create database` i `create table` eksportowane schemat tabeli w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="b4d7a-186">Tworzenie pliku formatu do opisywania tabeli Schemat danych eksportu/importu.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="b4d7a-187">Szczegóły pliku formatu są opisane w [Utwórz plik formatu (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="b4d7a-188">Generowanie pliku formatu podczas uruchamiania narzędzia BCP z komputera programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="b4d7a-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="b4d7a-189">Generowanie pliku formatu podczas uruchamiania narzędzia BCP zdalnie na serwerze SQL</span><span class="sxs-lookup"><span data-stu-id="b4d7a-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="b4d7a-190">Użyj jednej z metod opisanych w sekcji [przenoszenia danych z pliku źródłowego](#filesource_to_sqlonazurevm) przenoszenia danych w prostych plików do programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="b4d7a-191"><a name="sql-migration"></a>Kreator migracji bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b4d7a-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="b4d7a-192">[Kreator migracji bazy danych programu SQL Server](http://sqlazuremw.codeplex.com/) zapewnia przyjazną dla użytkownika sposób przenoszenia danych między dwa wystąpienia programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="b4d7a-193">Umożliwia użytkownikowi mapowanie schematu danych między źródłami a tabel docelowych, wybierz typy kolumn i różnych innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="b4d7a-194">Używa kopiowania zbiorczego (BCP) w obszarze obejmuje.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="b4d7a-195">Poniżej przedstawiono zrzut ekranu przedstawiający ekran powitalny Kreatora migracji bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![Kreator migracji programu SQL Server][2]

### <span data-ttu-id="b4d7a-197"><a name="sql-backup"></a>Baza danych kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="b4d7a-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="b4d7a-198">SQL Server obsługuje:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-198">SQL Server supports:</span></span>

1. <span data-ttu-id="b4d7a-199">[Baza danych kopii zapasowej i przywrócenia jej funkcjonalności](https://msdn.microsoft.com/library/ms187048.aspx) (zarówno do lokalnego pliku lub pliku bacpac Eksport do obiektu blob) i [aplikacji warstwy danych](https://msdn.microsoft.com/library/ee210546.aspx) (przy użyciu pliku bacpac).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="b4d7a-200">Możliwość bezpośrednio tworzenia maszyn wirtualnych programu SQL Server na platformie Azure za pomocą skopiowanego bazy danych lub Kopiuj do istniejącej bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="b4d7a-201">Aby uzyskać więcej informacji, zobacz [za pomocą Kreatora kopiowania bazy danych](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="b4d7a-202">Zrzut ekranu przedstawiający kopii bazy danych w górę/przywracania z programu SQL Server Management Studio opcje są wyświetlane poniżej.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Narzędzie importu programu SQL Server][1]

## <a name="resources"></a><span data-ttu-id="b4d7a-204">Zasoby</span><span class="sxs-lookup"><span data-stu-id="b4d7a-204">Resources</span></span>
[<span data-ttu-id="b4d7a-205">Migrowanie bazy danych do programu SQL Server na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b4d7a-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="b4d7a-206">Omówienie programu SQL Server w usłudze Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="b4d7a-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
