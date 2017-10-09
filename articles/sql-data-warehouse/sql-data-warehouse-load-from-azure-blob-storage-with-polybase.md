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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Ładowanie danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse (PolyBase)
> [!div class="op_single_selector"]
> * [Fabryka danych](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

Użyj T-SQL i PolyBase polecenia tooload danych z magazynu obiektów blob platformy Azure do usługi Azure SQL Data Warehouse. 

proste, w tym samouczku ładuje dwóch tabel z publicznego obiektu Blob magazynu Azure do schematu magazynu danych sprzedaży detalicznej Contoso hello tookeep. tooload hello pełny zestaw danych, uruchom przykład Witaj [obciążenia hello pełne hurtowni danych sprzedaży detalicznej Contoso] [ Load hello full Contoso Retail Data Warehouse] z repozytorium Microsoft SQL Server przykłady hello.

W tym samouczku obejmują:

1. Skonfiguruj tooload PolyBase z magazynu obiektów blob platformy Azure
2. Ładowanie danych publicznej do bazy danych
3. Optymalizacje należy wykonać po zakończeniu hello obciążenia.

## <a name="before-you-begin"></a>Przed rozpoczęciem
toorun tego samouczka potrzebne konto platformy Azure, która ma już bazę danych SQL Data Warehouse. Jeśli nie masz jeszcze to, zobacz [Tworzenie usługi SQL Data Warehouse][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Konfigurowanie hello źródła danych
Program PolyBase używa lokalizacji hello toodefine zewnętrznych obiektów T-SQL i atrybuty hello danych zewnętrznych. definicje obiektów zewnętrznych Hello są przechowywane w usłudze SQL Data Warehouse. Witaj same dane są przechowywane zewnętrznie.

### <a name="11-create-a-credential"></a>1.1. Utwórz poświadczenia
**Pomiń ten krok** ładowania danych publicznych hello Contoso. Nie potrzebujesz danych publicznych toohello bezpiecznego dostępu, ponieważ jest on już dostępny tooanyone

**Nie, Pomiń ten krok** korzystając z tego samouczka jako szablon dla ładowania danych użytkownika. tooaccess dane przy użyciu poświadczeń, hello Użyj następującego skryptu poświadczeń toocreate o zakresie bazy danych, a następnie użyć go w podczas definiowania hello lokalizację hello źródła danych.

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

Pomiń toostep 2.

### <a name="12-create-hello-external-data-source"></a>1.2. Utwórz hello zewnętrznego źródła danych
Użyj tej [Tworzenie zewnętrznego źródła danych] [ CREATE EXTERNAL DATA SOURCE] polecenia toostore lokalizacji hello hello danych i hello typu danych. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Jeśli wybierzesz toomake Twojego publiczne kontenery magazynu obiektów blob platformy azure, należy pamiętać, że właściciel danych hello zostanie naliczona danych opłaty za wyjście po danych pozostawia hello centrum danych. 
> 
> 

## <a name="2-configure-data-format"></a>2. Skonfiguruj format danych
Hello dane są przechowywane w plikach tekstowych w magazynie obiektów blob platformy Azure, a poszczególne pola są rozdzielone ogranicznika. Uruchom to [utworzyć EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] format hello toospecify polecenia hello danych w plikach tekstowych hello. Witaj dane firmy Contoso jest nieskompresowanych i rozdzielonych potoku.

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

## <a name="3-create-hello-external-tables"></a>3. Tworzenie tabel zewnętrznych hello
Określono hello danych źródła i format pliku, użytkownik jest tabel zewnętrznych hello toocreate gotowe. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Tworzenie schematu hello danych.
toocreate hello toostore miejscu dane firmy Contoso w bazie danych, Utwórz schemat.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Utwórz hello tabel zewnętrznych.
Uruchom ten skrypt hello toocreate DimProduct i FactOnlineSales tabel zewnętrznych. Wszystkie robimy tutaj definiowania nazwy kolumn i typy danych i powiązania ich lokalizacji toohello i format plików magazynu obiektów blob platformy Azure hello. definicji Hello są przechowywane w magazynie danych SQL i danych hello jest nadal hello obiektu Blob magazynu Azure.

Witaj **lokalizacji** parametr jest hello folderu w folderze głównym hello w hello obiektu Blob magazynu Azure. Są w innym folderze.

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

## <a name="4-load-hello-data"></a>4. Ładowanie danych hello
Brak danych zewnętrznych tooaccess różne sposoby.  Można zapytania na danych bezpośrednio z tabeli zewnętrznej hello, ładowanie danych hello do nowych tabel bazy danych lub dodać tabele bazy danych tooexisting danych zewnętrznych.  

### <a name="41-create-a-new-schema"></a>4.1. Tworzenie nowego schematu
CTAS tworzy nową tabelę, która zawiera dane.  Najpierw należy utworzyć schemat hello dane firmy contoso.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Ładowanie danych hello do nowych tabel
dane tooload platformy Azure z magazynu obiektów blob i zapisz go w tabeli wewnątrz bazy danych, użyj hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrukcji. Podczas ładowania z CTAS hello wykorzystanie silnie typizowane tabel zewnętrznych dane hello created.tooload tylko do nowych tabel, skorzystaj z jednej [CTAS] [ CTAS] instrukcji na tabelę. 
 
CTAS tworzy nową tabelę i wypełnia hello wyników w instrukcji select. CTAS definiuje hello nowej tabeli toohave hello tej samej kolumny i typy danych jak wyniki hello hello wybierz instrukcji. Po wybraniu wszystkich hello kolumn z tabeli zewnętrznej hello nowa tabela będzie repliki hello kolumn i typy danych w tabeli zewnętrznej hello.

W tym przykładzie utworzymy zarówno hello wymiaru i tabeli faktów hello jako skrótów rozproszonej tabel. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 śledzić postęp obciążenia hello
Możesz śledzić postęp hello obciążenia przy użyciu dynamicznych widoków zarządzania (widoków DMV). 

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

## <a name="5-optimize-columnstore-compression"></a>5. Optymalizacja magazynu kolumn kompresji
Domyślnie usługa SQL Data Warehouse przechowuje hello tabeli jako klastrowany indeks magazynu kolumn. Po zakończeniu obciążenia nie może być niektóre wiersze danych hello skompresowane w hello magazynu kolumn.  Brak z różnych powodów, dlaczego jest to możliwe. toolearn więcej, zobacz [Zarządzaj indeksami magazynu kolumn][manage columnstore indexes].

toooptimize wydajność zapytań i ich kompresji magazynu kolumn po załadowaniu, Odbuduj hello tabeli tooforce hello magazynu kolumn indeksu toocompress wszystkie wiersze hello. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Aby uzyskać więcej informacji na temat zachowania indeksy magazynu kolumn, zobacz hello [Zarządzaj indeksami magazynu kolumn] [ manage columnstore indexes] artykułu.

## <a name="6-optimize-statistics"></a>6. Optymalizacja statystyki
Najważniejsze dane statystyczne pojedynczej kolumny toocreate jest natychmiast po załadowaniu. Dostępne są niektóre opcje wyboru statystyk. Na przykład jeśli tworzenie statystyk pojedynczej kolumny w każdej kolumnie może potrwać toorebuild długo wszystkie statystyki hello. Jeśli wiesz, że niektóre kolumny nie będą toobe w predykatach kwerendy, można pominąć tworzenie statystyk na podstawie tych kolumn.

Jeśli zdecydujesz toocreate statystyki pojedynczej kolumny w każdej kolumnie każda tabela służy przykładowy kod procedury składowanej hello `prc_sqldw_create_stats` w hello [statystyki] [ statistics] artykułu.

Poniższy przykład Hello jest dobry punkt wyjścia do tworzenia statystyk. W każdej kolumnie w tabeli wymiarów hello i w każdej kolumnie łącząca w tabelach faktów hello tworzy statystyki pojedynczej kolumny. Później można dodać kolumny tabeli faktów tooother statystyki jednego lub wielu kolumn.

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

## <a name="achievement-unlocked"></a>Osiągnięcia odblokowane!
Publiczne dane zostały pomyślnie załadowane do magazynu danych SQL Azure. Dobra robota!

Można teraz uruchomić tabele hello przy użyciu kwerend, takich jak hello następujące kwerendy:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Następne kroki
tooload hello pełne hurtowni danych sprzedaży detalicznej Contoso danych, użyj skryptu hello w więcej porad programistycznych, zobacz [omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].

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
