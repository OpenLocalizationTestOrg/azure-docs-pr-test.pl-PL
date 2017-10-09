---
title: "aaaLoad z magazynu danych obiektów blob platformy Azure tooAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse PolyBase tooload dane platformy Azure z magazynu obiektów blob do magazynu danych SQL. Ładowanie kilku tabel z danych publicznej do schematu magazynu danych sprzedaży detalicznej Contoso hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="e2cf7-104">Ładowanie danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="e2cf7-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2cf7-105">Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="e2cf7-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="e2cf7-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e2cf7-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="e2cf7-107">Użyj T-SQL i PolyBase polecenia tooload danych z magazynu obiektów blob platformy Azure do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="e2cf7-108">proste, w tym samouczku ładuje dwóch tabel z publicznego obiektu Blob magazynu Azure do schematu magazynu danych sprzedaży detalicznej Contoso hello tookeep.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="e2cf7-109">tooload hello pełny zestaw danych, uruchom przykład Witaj [obciążenia hello pełne hurtowni danych sprzedaży detalicznej Contoso] [ Load hello full Contoso Retail Data Warehouse] z repozytorium Microsoft SQL Server przykłady hello.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="e2cf7-110">W tym samouczku obejmują:</span><span class="sxs-lookup"><span data-stu-id="e2cf7-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="e2cf7-111">Skonfiguruj tooload PolyBase z magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e2cf7-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="e2cf7-112">Ładowanie danych publicznej do bazy danych</span><span class="sxs-lookup"><span data-stu-id="e2cf7-112">Load public data into your database</span></span>
3. <span data-ttu-id="e2cf7-113">Optymalizacje należy wykonać po zakończeniu hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e2cf7-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e2cf7-114">Before you begin</span></span>
<span data-ttu-id="e2cf7-115">toorun tego samouczka potrzebne konto platformy Azure, która ma już bazę danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="e2cf7-116">Jeśli nie masz jeszcze to, zobacz [Tworzenie usługi SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e2cf7-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="e2cf7-117">1. Konfigurowanie hello źródła danych</span><span class="sxs-lookup"><span data-stu-id="e2cf7-117">1. Configure hello data source</span></span>
<span data-ttu-id="e2cf7-118">Program PolyBase używa lokalizacji hello toodefine zewnętrznych obiektów T-SQL i atrybuty hello danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="e2cf7-119">definicje obiektów zewnętrznych Hello są przechowywane w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="e2cf7-120">Witaj same dane są przechowywane zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="e2cf7-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-121">1.1.</span></span> <span data-ttu-id="e2cf7-122">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="e2cf7-122">Create a credential</span></span>
<span data-ttu-id="e2cf7-123">**Pomiń ten krok** ładowania danych publicznych hello Contoso.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="e2cf7-124">Nie potrzebujesz danych publicznych toohello bezpiecznego dostępu, ponieważ jest on już dostępny tooanyone</span><span class="sxs-lookup"><span data-stu-id="e2cf7-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="e2cf7-125">**Nie, Pomiń ten krok** korzystając z tego samouczka jako szablon dla ładowania danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="e2cf7-126">tooaccess dane przy użyciu poświadczeń, hello Użyj następującego skryptu poświadczeń toocreate o zakresie bazy danych, a następnie użyć go w podczas definiowania hello lokalizację hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

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
```

<span data-ttu-id="e2cf7-127">Pomiń toostep 2.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="e2cf7-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-128">1.2.</span></span> <span data-ttu-id="e2cf7-129">Utwórz hello zewnętrznego źródła danych</span><span class="sxs-lookup"><span data-stu-id="e2cf7-129">Create hello external data source</span></span>
<span data-ttu-id="e2cf7-130">Użyj tej [Tworzenie zewnętrznego źródła danych] [ CREATE EXTERNAL DATA SOURCE] polecenia toostore lokalizacji hello hello danych i hello typu danych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="e2cf7-131">Jeśli wybierzesz toomake Twojego publiczne kontenery magazynu obiektów blob platformy azure, należy pamiętać, że właściciel danych hello zostanie naliczona danych opłaty za wyjście po danych pozostawia hello centrum danych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="e2cf7-132">2. Skonfiguruj format danych</span><span class="sxs-lookup"><span data-stu-id="e2cf7-132">2. Configure data format</span></span>
<span data-ttu-id="e2cf7-133">Hello dane są przechowywane w plikach tekstowych w magazynie obiektów blob platformy Azure, a poszczególne pola są rozdzielone ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="e2cf7-134">Uruchom to [utworzyć EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] format hello toospecify polecenia hello danych w plikach tekstowych hello.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="e2cf7-135">Witaj dane firmy Contoso jest nieskompresowanych i rozdzielonych potoku.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="e2cf7-136">3. Tworzenie tabel zewnętrznych hello</span><span class="sxs-lookup"><span data-stu-id="e2cf7-136">3. Create hello external tables</span></span>
<span data-ttu-id="e2cf7-137">Określono hello danych źródła i format pliku, użytkownik jest tabel zewnętrznych hello toocreate gotowe.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="e2cf7-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-138">3.1.</span></span> <span data-ttu-id="e2cf7-139">Tworzenie schematu hello danych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-139">Create a schema for hello data.</span></span>
<span data-ttu-id="e2cf7-140">toocreate hello toostore miejscu dane firmy Contoso w bazie danych, Utwórz schemat.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="e2cf7-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-141">3.2.</span></span> <span data-ttu-id="e2cf7-142">Utwórz hello tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-142">Create hello external tables.</span></span>
<span data-ttu-id="e2cf7-143">Uruchom ten skrypt hello toocreate DimProduct i FactOnlineSales tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="e2cf7-144">Wszystkie robimy tutaj definiowania nazwy kolumn i typy danych i powiązania ich lokalizacji toohello i format plików magazynu obiektów blob platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="e2cf7-145">definicji Hello są przechowywane w magazynie danych SQL i danych hello jest nadal hello obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="e2cf7-146">Witaj **lokalizacji** parametr jest hello folderu w folderze głównym hello w hello obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="e2cf7-147">Są w innym folderze.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a><span data-ttu-id="e2cf7-148">4. Ładowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="e2cf7-148">4. Load hello data</span></span>
<span data-ttu-id="e2cf7-149">Brak danych zewnętrznych tooaccess różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="e2cf7-150">Można zapytania na danych bezpośrednio z tabeli zewnętrznej hello, ładowanie danych hello do nowych tabel bazy danych lub dodać tabele bazy danych tooexisting danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="e2cf7-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-151">4.1.</span></span> <span data-ttu-id="e2cf7-152">Tworzenie nowego schematu</span><span class="sxs-lookup"><span data-stu-id="e2cf7-152">Create a new schema</span></span>
<span data-ttu-id="e2cf7-153">CTAS tworzy nową tabelę, która zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="e2cf7-154">Najpierw należy utworzyć schemat hello dane firmy contoso.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="e2cf7-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-155">4.2.</span></span> <span data-ttu-id="e2cf7-156">Ładowanie danych hello do nowych tabel</span><span class="sxs-lookup"><span data-stu-id="e2cf7-156">Load hello data into new tables</span></span>
<span data-ttu-id="e2cf7-157">dane tooload platformy Azure z magazynu obiektów blob i zapisz go w tabeli wewnątrz bazy danych, użyj hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="e2cf7-158">Podczas ładowania z CTAS hello wykorzystanie silnie typizowane tabel zewnętrznych dane hello created.tooload tylko do nowych tabel, skorzystaj z jednej [CTAS] [ CTAS] instrukcji na tabelę.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="e2cf7-159">CTAS tworzy nową tabelę i wypełnia hello wyników w instrukcji select.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="e2cf7-160">CTAS definiuje hello nowej tabeli toohave hello tej samej kolumny i typy danych jak wyniki hello hello wybierz instrukcji.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="e2cf7-161">Po wybraniu wszystkich hello kolumn z tabeli zewnętrznej hello nowa tabela będzie repliki hello kolumn i typy danych w tabeli zewnętrznej hello.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="e2cf7-162">W tym przykładzie utworzymy zarówno hello wymiaru i tabeli faktów hello jako skrótów rozproszonej tabel.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="e2cf7-163">4.3 śledzić postęp obciążenia hello</span><span class="sxs-lookup"><span data-stu-id="e2cf7-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="e2cf7-164">Możesz śledzić postęp hello obciążenia przy użyciu dynamicznych widoków zarządzania (widoków DMV).</span><span class="sxs-lookup"><span data-stu-id="e2cf7-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="e2cf7-165">5. Optymalizacja magazynu kolumn kompresji</span><span class="sxs-lookup"><span data-stu-id="e2cf7-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="e2cf7-166">Domyślnie usługa SQL Data Warehouse przechowuje hello tabeli jako klastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="e2cf7-167">Po zakończeniu obciążenia nie może być niektóre wiersze danych hello skompresowane w hello magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="e2cf7-168">Brak z różnych powodów, dlaczego jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="e2cf7-169">toolearn więcej, zobacz [Zarządzaj indeksami magazynu kolumn][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="e2cf7-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="e2cf7-170">toooptimize wydajność zapytań i ich kompresji magazynu kolumn po załadowaniu, Odbuduj hello tabeli tooforce hello magazynu kolumn indeksu toocompress wszystkie wiersze hello.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="e2cf7-171">Aby uzyskać więcej informacji na temat zachowania indeksy magazynu kolumn, zobacz hello [Zarządzaj indeksami magazynu kolumn] [ manage columnstore indexes] artykułu.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="e2cf7-172">6. Optymalizacja statystyki</span><span class="sxs-lookup"><span data-stu-id="e2cf7-172">6. Optimize statistics</span></span>
<span data-ttu-id="e2cf7-173">Najważniejsze dane statystyczne pojedynczej kolumny toocreate jest natychmiast po załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="e2cf7-174">Dostępne są niektóre opcje wyboru statystyk.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-174">There are some choices for statistics.</span></span> <span data-ttu-id="e2cf7-175">Na przykład jeśli tworzenie statystyk pojedynczej kolumny w każdej kolumnie może potrwać toorebuild długo wszystkie statystyki hello.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="e2cf7-176">Jeśli wiesz, że niektóre kolumny nie będą toobe w predykatach kwerendy, można pominąć tworzenie statystyk na podstawie tych kolumn.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="e2cf7-177">Jeśli zdecydujesz toocreate statystyki pojedynczej kolumny w każdej kolumnie każda tabela służy przykładowy kod procedury składowanej hello `prc_sqldw_create_stats` w hello [statystyki] [ statistics] artykułu.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="e2cf7-178">Poniższy przykład Hello jest dobry punkt wyjścia do tworzenia statystyk.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="e2cf7-179">W każdej kolumnie w tabeli wymiarów hello i w każdej kolumnie łącząca w tabelach faktów hello tworzy statystyki pojedynczej kolumny.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="e2cf7-180">Później można dodać kolumny tabeli faktów tooother statystyki jednego lub wielu kolumn.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="e2cf7-181">Osiągnięcia odblokowane!</span><span class="sxs-lookup"><span data-stu-id="e2cf7-181">Achievement unlocked!</span></span>
<span data-ttu-id="e2cf7-182">Publiczne dane zostały pomyślnie załadowane do magazynu danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e2cf7-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e2cf7-183">Dobra robota!</span><span class="sxs-lookup"><span data-stu-id="e2cf7-183">Great job!</span></span>

<span data-ttu-id="e2cf7-184">Można teraz uruchomić tabele hello przy użyciu kwerend, takich jak hello następujące kwerendy:</span><span class="sxs-lookup"><span data-stu-id="e2cf7-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="e2cf7-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2cf7-185">Next steps</span></span>
<span data-ttu-id="e2cf7-186">tooload hello pełne hurtowni danych sprzedaży detalicznej Contoso danych, użyj skryptu hello w więcej porad programistycznych, zobacz [omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e2cf7-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
