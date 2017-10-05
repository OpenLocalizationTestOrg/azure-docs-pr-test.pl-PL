---
title: "Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (PolyBase) | Microsoft Docs"
description: "Eksportowanie danych z programu SQL Server do plików prostych przy użyciu programu bcpw, importowanie danych do usługi Azure Blob Storage przy użyciu programu AZCopy oraz pozyskiwanie danych do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 860c86e0-90f7-492c-9a84-1bdd3d1735cd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 966100094f98bae41bf90df500d005fa78b31ec3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="6638e-103">Ładowanie danych przy użyciu programu PolyBase w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6638e-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6638e-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="6638e-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="6638e-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="6638e-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="6638e-106">bcp</span><span class="sxs-lookup"><span data-stu-id="6638e-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="6638e-107">Ten samouczek przedstawia sposób ładowania danych do usługi SQL Data Warehouse przy użyciu programów AzCopy i PolyBase.</span><span class="sxs-lookup"><span data-stu-id="6638e-107">This tutorial shows how to load data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="6638e-108">Po zakończeniu będziesz umieć wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6638e-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="6638e-109">Kopiowanie danych do magazynu obiektów blob platformy Azure przy użyciu programu AzCopy</span><span class="sxs-lookup"><span data-stu-id="6638e-109">Use AzCopy to copy data to Azure blob storage</span></span>
* <span data-ttu-id="6638e-110">Tworzenie obiektów bazy danych do definiowania danych</span><span class="sxs-lookup"><span data-stu-id="6638e-110">Create database objects to define the data</span></span>
* <span data-ttu-id="6638e-111">Uruchamianie zapytania T-SQL do ładowania danych</span><span class="sxs-lookup"><span data-stu-id="6638e-111">Run a T-SQL query to load the data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6638e-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6638e-112">Prerequisites</span></span>
<span data-ttu-id="6638e-113">Do wykonania kroków opisanych w tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="6638e-113">To step through this tutorial, you need</span></span>

* <span data-ttu-id="6638e-114">Baza danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6638e-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="6638e-115">Konto magazynu platformy Azure typu standardowy magazyn lokalnie nadmiarowy (Standard-LRS), standardowy magazyn geograficznie nadmiarowy (Standard-GRS) lub standardowy magazyn geograficznie nadmiarowy dostępny do odczytu (Standard-RAGRS).</span><span class="sxs-lookup"><span data-stu-id="6638e-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="6638e-116">Narzędzie wiersza polecenia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="6638e-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="6638e-117">Pobierz i zainstaluj [najnowszą wersję programu AzCopy][latest version of AzCopy], która jest instalowana z narzędziami Microsoft Azure Storage Tools.</span><span class="sxs-lookup"><span data-stu-id="6638e-117">Download and install the [latest version of AzCopy][latest version of AzCopy] which is installed with the Microsoft Azure Storage Tools.</span></span>
  
    ![Narzędzia Azure Storage Tools](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-to-azure-blob-storage"></a><span data-ttu-id="6638e-119">Krok 1: dodawanie przykładowych danych do magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6638e-119">Step 1: Add sample data to Azure blob storage</span></span>
<span data-ttu-id="6638e-120">Aby załadować dane, trzeba umieścić trochę przykładowych danych w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6638e-120">In order to load data, we need to put some sample data into an Azure blob storage.</span></span> <span data-ttu-id="6638e-121">W tym kroku wypełnimy obiekt blob magazynu Azure przykładowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="6638e-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="6638e-122">Następnie użyjemy aparatu PolyBase, aby załadować te przykładowe dane do bazy danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6638e-122">Later, we will use PolyBase to load this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="6638e-123">A.</span><span class="sxs-lookup"><span data-stu-id="6638e-123">A.</span></span> <span data-ttu-id="6638e-124">Przygotowanie przykładowego pliku tekstowego</span><span class="sxs-lookup"><span data-stu-id="6638e-124">Prepare a sample text file</span></span>
<span data-ttu-id="6638e-125">Aby przygotować przykładowy plik tekstowy:</span><span class="sxs-lookup"><span data-stu-id="6638e-125">To prepare a sample text file:</span></span>

1. <span data-ttu-id="6638e-126">Otwórz program Notatnik i skopiuj następujące wiersze danych do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="6638e-126">Open Notepad and copy the following lines of data into a new file.</span></span> <span data-ttu-id="6638e-127">Zapisz go jako % temp%\DimDate2.txt w lokalnym katalogu tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="6638e-127">Save this to your local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="6638e-128">B.</span><span class="sxs-lookup"><span data-stu-id="6638e-128">B.</span></span> <span data-ttu-id="6638e-129">Znajdowanie punktu końcowego usługi Blob</span><span class="sxs-lookup"><span data-stu-id="6638e-129">Find your blob service endpoint</span></span>
<span data-ttu-id="6638e-130">Aby znaleźć punkt końcowy usługi Blob:</span><span class="sxs-lookup"><span data-stu-id="6638e-130">To find your blob service endpoint:</span></span>

1. <span data-ttu-id="6638e-131">W Portalu Azure wybierz opcje **Przeglądaj**  >  **Konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="6638e-131">From the Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="6638e-132">Kliknij konto magazynu, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="6638e-132">Click the storage account you want to use.</span></span>
3. <span data-ttu-id="6638e-133">W bloku Konto magazynu kliknij pozycję Obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="6638e-133">In the Storage account blade, click Blobs</span></span>
   
    ![Klikanie pozycji Obiekty blob](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="6638e-135">Zapisz adres URL punktu końcowego usługi Blob do użycia później.</span><span class="sxs-lookup"><span data-stu-id="6638e-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Punkt końcowy usługi Blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="6638e-137">C.</span><span class="sxs-lookup"><span data-stu-id="6638e-137">C.</span></span> <span data-ttu-id="6638e-138">Znajdowanie klucza magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="6638e-138">Find your Azure storage key</span></span>
<span data-ttu-id="6638e-139">Aby znaleźć klucz magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="6638e-139">To find your Azure storage key:</span></span>

1. <span data-ttu-id="6638e-140">W witrynie Azure Portal wybierz opcje **Przeglądaj** > **Konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="6638e-140">From the Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="6638e-141">Kliknij konto magazynu, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="6638e-141">Click on the storage account you want to use.</span></span>
3. <span data-ttu-id="6638e-142">Wybierz pozycje **Wszystkie ustawienia**  >  **Klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="6638e-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="6638e-143">Kliknij pole kopiowania, aby skopiować jeden z kluczy dostępu do schowka.</span><span class="sxs-lookup"><span data-stu-id="6638e-143">Click the copy box to copy one of your access keys to the clipboard.</span></span>
   
    ![Kopiowanie klucza magazynu Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-the-sample-file-to-azure-blob-storage"></a><span data-ttu-id="6638e-145">D.</span><span class="sxs-lookup"><span data-stu-id="6638e-145">D.</span></span> <span data-ttu-id="6638e-146">Kopiowanie przykładowego pliku do magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6638e-146">Copy the sample file to Azure blob storage</span></span>
<span data-ttu-id="6638e-147">Aby skopiować dane do magazynu obiektów blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6638e-147">To copy your data to Azure blob storage:</span></span>

1. <span data-ttu-id="6638e-148">Otwórz wiersz polecenia i zmień katalogi na katalog instalacyjny programu AzCopy.</span><span class="sxs-lookup"><span data-stu-id="6638e-148">Open a command prompt, and change directories to the AzCopy installation directory.</span></span> <span data-ttu-id="6638e-149">To polecenie powoduje zmianę domyślnego katalogu instalacji na 64-bitowym kliencie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6638e-149">This command changes to the default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="6638e-150">Uruchom następujące polecenie, aby przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="6638e-150">Run the following command to upload the file.</span></span> <span data-ttu-id="6638e-151">Określ adres URL punktu końcowego usługi Blob jako wartość <blob service endpoint URL> i klucz konta usługi Azure Storage jako wartość <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="6638e-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="6638e-152">Zobacz też: [Wprowadzenie do narzędzia wiersza polecenia AzCopy][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="6638e-152">See also [Getting Started with the AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="6638e-153">E.</span><span class="sxs-lookup"><span data-stu-id="6638e-153">E.</span></span> <span data-ttu-id="6638e-154">Eksplorowanie kontenera magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="6638e-154">Explore your blob storage container</span></span>
<span data-ttu-id="6638e-155">Aby zobaczyć plik przekazany do magazynu obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="6638e-155">To see the file you uploaded to blob storage:</span></span>

1. <span data-ttu-id="6638e-156">Wróć do bloku usługi Blob.</span><span class="sxs-lookup"><span data-stu-id="6638e-156">Go back to your Blob service blade.</span></span>
2. <span data-ttu-id="6638e-157">W obszarze Kontenery kliknij dwukrotnie pozycję **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="6638e-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="6638e-158">Aby wyświetlić ścieżkę do danych, kliknij folder **datedimension**, w którym będzie widoczny przekazany plik **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="6638e-158">To explore the path to your data, click the folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="6638e-159">Aby wyświetlić właściwości, kliknij plik **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="6638e-159">To view properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="6638e-160">Zauważ, że w bloku właściwości obiektu blob można pobrać lub usunąć plik.</span><span class="sxs-lookup"><span data-stu-id="6638e-160">Note that in the Blob properties blade, you can download or delete the file.</span></span>
   
    ![Wyświetlanie obiektu blob magazynu Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-the-sample-data"></a><span data-ttu-id="6638e-162">Krok 2: tworzenie tabeli zewnętrznej dla przykładowych danych</span><span class="sxs-lookup"><span data-stu-id="6638e-162">Step 2: Create an external table for the sample data</span></span>
<span data-ttu-id="6638e-163">W tej sekcji utworzymy tabelę zewnętrzną definiującą przykładowe dane.</span><span class="sxs-lookup"><span data-stu-id="6638e-163">In this section we create an external table that defines the sample data.</span></span>

<span data-ttu-id="6638e-164">Aparat PolyBase używa tabel zewnętrznych do uzyskiwania dostępu do danych w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6638e-164">PolyBase uses external tables to access data in Azure blob storage.</span></span> <span data-ttu-id="6638e-165">Ponieważ dane nie są przechowywane w usłudze SQL Data Warehouse, aparat PolyBase obsługuje uwierzytelnianie w odniesieniu do danych zewnętrznych przy użyciu poświadczeń o zakresie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6638e-165">Since the data is not stored within SQL Data Warehouse, PolyBase handles authentication to the external data by using a database-scoped credential.</span></span>

<span data-ttu-id="6638e-166">W tym kroku przykładu użyto następujących instrukcji języka Transact-SQL do utworzenia tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="6638e-166">The example in this step uses these Transact-SQL statements to create an external table.</span></span>

* <span data-ttu-id="6638e-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] w celu szyfrowania wpisu tajnego poświadczeń o zakresie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6638e-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] to encrypt the secret of your database scoped credential.</span></span>
* <span data-ttu-id="6638e-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)], aby określić dane uwierzytelniania dla konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6638e-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] to specify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="6638e-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)], aby określić lokalizację usługi Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="6638e-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] to specify the location of your Azure blob storage.</span></span>
* <span data-ttu-id="6638e-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)], aby określić format danych.</span><span class="sxs-lookup"><span data-stu-id="6638e-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] to specify the format of your data.</span></span>
* <span data-ttu-id="6638e-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)], aby określić definicję tabeli i lokalizację danych.</span><span class="sxs-lookup"><span data-stu-id="6638e-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] to specify the table definition and location of the data.</span></span>

<span data-ttu-id="6638e-172">Uruchom to zapytanie w bazie danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6638e-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="6638e-173">W schemacie dbo zostanie utworzona zewnętrzna tabela o nazwie DimDate2External wskazująca przykładowe dane DimDate2.txt w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6638e-173">It will create an external table named DimDate2External in the dbo schema that points to the DimDate2.txt sample data in the Azure blob storage.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

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


-- E: Create the external table
-- Specify column names and data types. This needs to match the data in the sample file.
-- LOCATION: Specify path to file or directory that contains the data (relative to the blob container).
-- To point to all files under the blob container, use LOCATION='.'

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


-- Run a query on the external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="6638e-174">W Eksploratorze obiektów SQL Server w programie Visual Studio widoczne będą: format pliku zewnętrznego, zewnętrzne źródło danych oraz tabela DimDate2External.</span><span class="sxs-lookup"><span data-stu-id="6638e-174">In SQL Server Object Explorer in Visual Studio, you can see the external file format, external data source, and the DimDate2External table.</span></span>

![Widok tabeli zewnętrznej](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="6638e-176">Krok 3: ładowanie danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6638e-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="6638e-177">Po utworzeniu tabeli zewnętrznej można załadować dane do nowej tabeli lub wstawić je do tabeli istniejącej.</span><span class="sxs-lookup"><span data-stu-id="6638e-177">Once the external table is created, you can either load the data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="6638e-178">Aby załadować dane do nowej tabeli, uruchom instrukcję [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="6638e-178">To load the data into a new table, run the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="6638e-179">Nowa tabela będzie miała kolumny o nazwach podanych w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="6638e-179">The new table will have the columns named in the query.</span></span> <span data-ttu-id="6638e-180">Typy danych kolumn będą zgodne z typami danych w definicji tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="6638e-180">The data types of the columns will match the data types in the external table definition.</span></span>
* <span data-ttu-id="6638e-181">Aby załadować dane do istniejącej tabeli, użyj instrukcji [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="6638e-181">To load the data into an existing table, use the [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load the data from Azure blob storage to SQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="6638e-182">Krok 4: tworzenie statystyk na podstawie nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="6638e-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="6638e-183">Usługa SQL Data Warehouse nie tworzy ani nie aktualizuje statystyk w sposób automatyczny.</span><span class="sxs-lookup"><span data-stu-id="6638e-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="6638e-184">Dlatego, aby uzyskać wysoką wydajność zapytań, ważne jest tworzenie statystyk dotyczących poszczególnych kolumn każdej tabeli po pierwszym załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="6638e-184">Therefore, to achieve high query performance, it's important to create statistics on each column of each table after the first load.</span></span> <span data-ttu-id="6638e-185">Istotne jest również aktualizowanie statystyk po wprowadzeniu istotnych zmian w danych.</span><span class="sxs-lookup"><span data-stu-id="6638e-185">It's also important to update statistics after substantial changes in the data.</span></span>

<span data-ttu-id="6638e-186">W tym przykładzie zostaną utworzone statystyki dla pojedynczej kolumny w nowej tabeli DimDate2.</span><span class="sxs-lookup"><span data-stu-id="6638e-186">This example creates single-column statistics on the new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="6638e-187">Aby dowiedzieć się więcej, zobacz temat [Statystyki][Statistics].</span><span class="sxs-lookup"><span data-stu-id="6638e-187">To learn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6638e-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6638e-188">Next steps</span></span>
<span data-ttu-id="6638e-189">Zobacz [Przewodnik po programie PolyBase][PolyBase guide] w celu uzyskania dalszych informacji przydatnych podczas tworzenia rozwiązań z użyciem aparatu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="6638e-189">See the [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
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
