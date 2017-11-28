---
title: "aaaPolyBase w SQL Data Warehouse — samouczek | Dokumentacja firmy Microsoft"
description: "Dowiedz się, co to jest aparat PolyBase i jak toouse go w scenariuszach dotyczących magazynów danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="17b00-103">Ładowanie danych przy użyciu programu PolyBase w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="17b00-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17b00-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="17b00-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="17b00-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="17b00-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="17b00-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="17b00-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="17b00-107">BCP</span><span class="sxs-lookup"><span data-stu-id="17b00-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="17b00-108">Ten samouczek pokazuje, jak tooload danych do usługi SQL Data Warehouse przy użyciu programów AzCopy i PolyBase.</span><span class="sxs-lookup"><span data-stu-id="17b00-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="17b00-109">Po zakończeniu będziesz umieć wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17b00-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="17b00-110">Użyj magazynu obiektów blob tooAzure AzCopy toocopy danych</span><span class="sxs-lookup"><span data-stu-id="17b00-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="17b00-111">Tworzenie obiektów bazy danych toodefine hello danych</span><span class="sxs-lookup"><span data-stu-id="17b00-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="17b00-112">Uruchamianie zapytania T-SQL tooload hello danych</span><span class="sxs-lookup"><span data-stu-id="17b00-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="17b00-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="17b00-113">Prerequisites</span></span>
<span data-ttu-id="17b00-114">toostep opisanych w tym samouczku, należy</span><span class="sxs-lookup"><span data-stu-id="17b00-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="17b00-115">Baza danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17b00-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="17b00-116">Konto magazynu platformy Azure typu standardowy magazyn lokalnie nadmiarowy (Standard-LRS), standardowy magazyn geograficznie nadmiarowy (Standard-GRS) lub standardowy magazyn geograficznie nadmiarowy dostępny do odczytu (Standard-RAGRS).</span><span class="sxs-lookup"><span data-stu-id="17b00-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="17b00-117">Narzędzie wiersza polecenia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="17b00-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="17b00-118">Pobierz i zainstaluj hello [najnowszą wersję programu AzCopy] [ latest version of AzCopy] który został zainstalowany z hello narzędzia magazynu usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="17b00-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Narzędzia Azure Storage Tools](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="17b00-120">Krok 1: Dodawanie przykładowych danych tooAzure obiektu blob magazynu</span><span class="sxs-lookup"><span data-stu-id="17b00-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="17b00-121">W danych tooload potrzebujemy tooput przykładowych danych do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17b00-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="17b00-122">W tym kroku wypełnimy obiekt blob magazynu Azure przykładowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="17b00-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="17b00-123">Później użyjemy PolyBase tooload przykładowe dane do bazy danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17b00-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="17b00-124">A.</span><span class="sxs-lookup"><span data-stu-id="17b00-124">A.</span></span> <span data-ttu-id="17b00-125">Przygotowanie przykładowego pliku tekstowego</span><span class="sxs-lookup"><span data-stu-id="17b00-125">Prepare a sample text file</span></span>
<span data-ttu-id="17b00-126">Przykładowy plik tekstowy tooprepare:</span><span class="sxs-lookup"><span data-stu-id="17b00-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="17b00-127">Otwórz Notatnik i skopiuj hello następujące wiersze danych do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="17b00-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="17b00-128">Zapisz ten tooyour lokalnym katalogu tymczasowym jako % temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="17b00-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="17b00-129">B.</span><span class="sxs-lookup"><span data-stu-id="17b00-129">B.</span></span> <span data-ttu-id="17b00-130">Znajdowanie punktu końcowego usługi Blob</span><span class="sxs-lookup"><span data-stu-id="17b00-130">Find your blob service endpoint</span></span>
<span data-ttu-id="17b00-131">toofind punktu końcowego usługi blob:</span><span class="sxs-lookup"><span data-stu-id="17b00-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="17b00-132">Z hello portalu Azure wybierz **Przeglądaj** > **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="17b00-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="17b00-133">Kliknij przycisk hello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="17b00-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="17b00-134">W bloku konto magazynu hello kliknij pozycję obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="17b00-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Klikanie pozycji Obiekty blob](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="17b00-136">Zapisz adres URL punktu końcowego usługi Blob do użycia później.</span><span class="sxs-lookup"><span data-stu-id="17b00-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Punkt końcowy usługi Blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="17b00-138">C.</span><span class="sxs-lookup"><span data-stu-id="17b00-138">C.</span></span> <span data-ttu-id="17b00-139">Znajdowanie klucza magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="17b00-139">Find your Azure storage key</span></span>
<span data-ttu-id="17b00-140">toofind klucza magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="17b00-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="17b00-141">Z hello portalu Azure, wybierz **Przeglądaj** > **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="17b00-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="17b00-142">Polecenie hello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="17b00-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="17b00-143">Wybierz pozycje **Wszystkie ustawienia**  >  **Klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="17b00-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="17b00-144">Kliknij przycisk hello toocopy pole kopiowania, jeden Schowka toohello klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="17b00-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Kopiowanie klucza magazynu Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="17b00-146">D.</span><span class="sxs-lookup"><span data-stu-id="17b00-146">D.</span></span> <span data-ttu-id="17b00-147">Skopiuj magazynu obiektów blob tooAzure hello przykładowych plików</span><span class="sxs-lookup"><span data-stu-id="17b00-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="17b00-148">toocopy usługi magazynu obiektów blob tooAzure danych:</span><span class="sxs-lookup"><span data-stu-id="17b00-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="17b00-149">Otwórz wiersz polecenia i zmień katalog instalacyjny AzCopy toohello katalogów.</span><span class="sxs-lookup"><span data-stu-id="17b00-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="17b00-150">To polecenie powoduje zmianę domyślnego katalogu instalacji na komputerze klienckim systemu Windows w 64-bitowych toohello.</span><span class="sxs-lookup"><span data-stu-id="17b00-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="17b00-151">Uruchom poniższe polecenie tooupload hello plik hello.</span><span class="sxs-lookup"><span data-stu-id="17b00-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="17b00-152">Określ adres URL punktu końcowego usługi Blob jako wartość <blob service endpoint URL> i klucz konta usługi Azure Storage jako wartość <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="17b00-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="17b00-153">Zobacz też [wprowadzenie hello wiersza polecenia Azcopy][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="17b00-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="17b00-154">E.</span><span class="sxs-lookup"><span data-stu-id="17b00-154">E.</span></span> <span data-ttu-id="17b00-155">Eksplorowanie kontenera magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="17b00-155">Explore your blob storage container</span></span>
<span data-ttu-id="17b00-156">Plik hello toosee przekazać tooblob magazynu:</span><span class="sxs-lookup"><span data-stu-id="17b00-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="17b00-157">Przejdź wstecz bloku usługi Blob tooyour.</span><span class="sxs-lookup"><span data-stu-id="17b00-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="17b00-158">W obszarze Kontenery kliknij dwukrotnie pozycję **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="17b00-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="17b00-159">dane tooyour tooexplore hello ścieżki, kliknij hello folder **datedimension** i będzie widoczny przekazany plik **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="17b00-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="17b00-160">Kliknij przycisk Właściwości tooview **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="17b00-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="17b00-161">Należy pamiętać, że w bloku właściwości obiektu Blob hello, można pobrać lub usunąć hello pliku.</span><span class="sxs-lookup"><span data-stu-id="17b00-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Wyświetlanie obiektu blob magazynu Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="17b00-163">Krok 2: Tworzenie tabeli zewnętrznej hello przykładowych danych</span><span class="sxs-lookup"><span data-stu-id="17b00-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="17b00-164">W tej sekcji utworzymy tabelę zewnętrzną definiującą hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="17b00-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="17b00-165">Program PolyBase używa tabel zewnętrznych tooaccess danych w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17b00-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="17b00-166">Ponieważ hello dane nie są przechowywane w usłudze SQL Data Warehouse, aparat PolyBase obsługuje dane zewnętrzne toohello uwierzytelniania przy użyciu poświadczeń o zakresie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="17b00-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="17b00-167">przykład Witaj w tym kroku używa tych toocreate instrukcji języka Transact-SQL tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="17b00-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="17b00-168">[Tworzenie klucza głównego (Transact-SQL)] [ Create Master Key (Transact-SQL)] poświadczeń o zakresie klucz tajny hello tooencrypt bazy danych.</span><span class="sxs-lookup"><span data-stu-id="17b00-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="17b00-169">[Create Database Scoped Credential (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informacje dotyczące uwierzytelniania dla konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="17b00-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="17b00-170">[Create External Data Source (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify hello lokalizacji magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17b00-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="17b00-171">[Create External File Format (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify hello format danych.</span><span class="sxs-lookup"><span data-stu-id="17b00-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="17b00-172">[Create External Table (Transact-SQL)] [ Create External Table (Transact-SQL)] definicji tabeli hello toospecify i lokalizację hello danych.</span><span class="sxs-lookup"><span data-stu-id="17b00-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="17b00-173">Uruchom to zapytanie w bazie danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17b00-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="17b00-174">Zostanie utworzony o nazwie DimDate2External w schemacie dbo hello wskazujące przykładowe dane DimDate2.txt toohello w magazynie obiektów blob Azure hello tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="17b00-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="17b00-175">W Eksploratorze obiektów SQL Server w programie Visual Studio mogą zobaczyć hello format pliku zewnętrznego, zewnętrzne źródło danych i tabela DimDate2External hello.</span><span class="sxs-lookup"><span data-stu-id="17b00-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Widok tabeli zewnętrznej](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="17b00-177">Krok 3: ładowanie danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="17b00-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="17b00-178">Po utworzeniu tabeli zewnętrznej hello można załadować danych hello do nowej tabeli lub wstawić je do istniejącej tabeli.</span><span class="sxs-lookup"><span data-stu-id="17b00-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="17b00-179">tooload hello danych do nowej tabeli, uruchom hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="17b00-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="17b00-180">Witaj nowa tabela będzie miała hello kolumny o nazwie w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="17b00-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="17b00-181">typy danych Hello hello kolumn będą zgodne hello typów danych w definicji tabeli zewnętrznej hello.</span><span class="sxs-lookup"><span data-stu-id="17b00-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="17b00-182">tooload hello danych w istniejącej tabeli, użyj hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="17b00-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="17b00-183">Krok 4: tworzenie statystyk na podstawie nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="17b00-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="17b00-184">Usługa SQL Data Warehouse nie tworzy ani nie aktualizuje statystyk w sposób automatyczny.</span><span class="sxs-lookup"><span data-stu-id="17b00-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="17b00-185">W związku z tym tooachieve wysoką wydajność zapytań, ważne jest, najpierw załadować toocreate statystyk dotyczących poszczególnych kolumn każdej tabeli po hello.</span><span class="sxs-lookup"><span data-stu-id="17b00-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="17b00-186">Możliwe jest również tooupdate ważnych statystyk po wprowadzeniu istotnych zmian w danych hello.</span><span class="sxs-lookup"><span data-stu-id="17b00-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="17b00-187">Ten przykład tworzy statystyki pojedynczej kolumny hello nowej tabeli DimDate2.</span><span class="sxs-lookup"><span data-stu-id="17b00-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="17b00-188">toolearn więcej, zobacz [statystyki][Statistics].</span><span class="sxs-lookup"><span data-stu-id="17b00-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="17b00-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17b00-189">Next steps</span></span>
<span data-ttu-id="17b00-190">Zobacz hello [Przewodnik po programie PolyBase] [ PolyBase guide] dalszych informacji przydatnych podczas tworzenia rozwiązań z użyciem aparatu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="17b00-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
