---
title: "aaaCreate tabeli jako wybierz (CTAS) w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące programowania z hello Utwórz tabelę jako select — instrukcja (CTAS) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="6f992-103">Utwórz tabelę jako Select (CTAS) w magazynie danych SQL</span><span class="sxs-lookup"><span data-stu-id="6f992-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="6f992-104">Utwórz tabelę jako wybierz lub `CTAS` jest jednym z hello najważniejszych funkcjach T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6f992-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="6f992-105">Jest całkowicie zrównoleglone operacja, która tworzy nową tabelę oparte na danych wyjściowych hello instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="6f992-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="6f992-106">`CTAS`jest toocreate najprostszym i najszybszym sposobem hello kopii tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f992-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="6f992-107">Ten dokument zawiera zarówno przykłady i najlepsze rozwiązania dotyczące `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="6f992-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="6f992-108">WYBIERZ... W wersji programu vs. CTAS</span><span class="sxs-lookup"><span data-stu-id="6f992-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="6f992-109">Można rozważyć `CTAS` nadrzędne obciążona wersja `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="6f992-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="6f992-110">Poniżej przedstawiono przykładowy prostą `SELECT..INTO` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="6f992-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="6f992-111">W powyższym przykładzie hello `[dbo].[FactInternetSales_new]` zostałyby utworzone ROUND_ROBIN rozproszonej tabeli z INDEKSEM magazynu kolumn w KLASTRZE na nim są one wartości domyślnych tabeli hello w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6f992-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="6f992-112">`SELECT..INTO`jednak nie pozwala toochange wpisz albo hello dystrybucji metody lub hello indeks jako część hello operacji.</span><span class="sxs-lookup"><span data-stu-id="6f992-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="6f992-113">Jest to, gdy `CTAS` polega na.</span><span class="sxs-lookup"><span data-stu-id="6f992-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="6f992-114">tooconvert hello powyżej za`CTAS` jest dość proste:</span><span class="sxs-lookup"><span data-stu-id="6f992-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="6f992-115">Z `CTAS` są możliwe toochange zarówno hello dystrybucji hello tabeli danych, a także hello typ tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f992-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="6f992-116">Jeśli chcesz tylko toochange hello indeksu w Twojej `CTAS` operacji i hello tabela źródłowa jest rozpowszechniane skrót, a następnie z `CTAS` wykona operację najlepiej, jeśli hello tego samego typu kolumny i danych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="6f992-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="6f992-117">Pozwoli to uniknąć cross przenoszenia danych dystrybucji podczas operacji hello, które jest bardziej wydajny.</span><span class="sxs-lookup"><span data-stu-id="6f992-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="6f992-118">Przy użyciu toocopy CTAS tabeli</span><span class="sxs-lookup"><span data-stu-id="6f992-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="6f992-119">Możliwe, że jedną z najbardziej typowych hello korzysta z `CTAS` jest tworzenie kopii tabeli, dzięki czemu można zmienić hello DDL.</span><span class="sxs-lookup"><span data-stu-id="6f992-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="6f992-120">Jeśli na przykład pierwotnie utworzona jako tabela `ROUND_ROBIN` a teraz chcesz je zmienić tabeli tooa od kolumny, `CTAS` się, jak można zmienić kolumny dystrybucji hello.</span><span class="sxs-lookup"><span data-stu-id="6f992-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="6f992-121">`CTAS`można także toochange używane typy partycjonowania, indeksowania lub kolumny.</span><span class="sxs-lookup"><span data-stu-id="6f992-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="6f992-122">Załóżmy, że utworzono tej tabeli za pomocą typu dystrybucji domyślne hello `ROUND_ROBIN` rozproszonych, ponieważ kolumna nie dystrybucji została określona w hello `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="6f992-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="6f992-123">Teraz ma toocreate nową kopię tej tabeli z indeksem magazynu kolumn w klastrze tak, aby można było korzystać z wydajności hello tabel klastrowanego magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="6f992-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="6f992-124">Należy zawsze toodistribute tej tabeli po klucz produktu od są przewidywanie sprzężenia od tej kolumny, a ma tooavoid przenoszenia danych podczas sprzężenia na klucz produktu.</span><span class="sxs-lookup"><span data-stu-id="6f992-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="6f992-125">Na koniec ma również tooadd partycjonowania na OrderDateKey, dzięki czemu można szybko usunąć stare dane przez usunięcie starego partycji.</span><span class="sxs-lookup"><span data-stu-id="6f992-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="6f992-126">Oto hello CTAS instrukcja, która będzie skopiować starego tabeli do nowej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f992-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="6f992-127">Na koniec można zmienić Twojego tooswap tabel w nowej tabeli, a następnie upuść starego tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f992-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="6f992-128">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="6f992-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="6f992-129">W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello.</span><span class="sxs-lookup"><span data-stu-id="6f992-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="6f992-130">Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów.</span><span class="sxs-lookup"><span data-stu-id="6f992-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="6f992-131">Przy użyciu toowork CTAS wokół nieobsługiwane funkcje</span><span class="sxs-lookup"><span data-stu-id="6f992-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="6f992-132">`CTAS`może być również używane toowork wokół szereg funkcji hello nieobsługiwany wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="6f992-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="6f992-133">To może często udowodnić toobe sytuacji win/win nie tylko kodzie będą zgodne, ale będą często wykonywane szybciej na magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6f992-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="6f992-134">Jest to wyniku pełni zrównoleglone projekt.</span><span class="sxs-lookup"><span data-stu-id="6f992-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="6f992-135">Scenariusze, które można pracować z CTAS wokół obejmują:</span><span class="sxs-lookup"><span data-stu-id="6f992-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="6f992-136">SPRZĘŻENIA ANSI na aktualizacje</span><span class="sxs-lookup"><span data-stu-id="6f992-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="6f992-137">Sprzężenia ANSI na usuwaniu</span><span class="sxs-lookup"><span data-stu-id="6f992-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="6f992-138">MERGE — instrukcja</span><span class="sxs-lookup"><span data-stu-id="6f992-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="6f992-139">Spróbuj toothink "CTAS pierwszy".</span><span class="sxs-lookup"><span data-stu-id="6f992-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="6f992-140">Jeśli uważasz, że uda się rozwiązać problem przy użyciu `CTAS` hello najlepsze sposób tooapproach zazwyczaj jest to go — nawet jeśli w związku z tym pisania większej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="6f992-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="6f992-141">ANSI zamienny sprzężenia dla instrukcji update</span><span class="sxs-lookup"><span data-stu-id="6f992-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="6f992-142">Może się okazać się, że masz złożonych aktualizacji, której jest przyłączany więcej niż dwie tabele ze sobą przy użyciu ANSI dołączenie hello tooperform składni UPDATE lub DELETE.</span><span class="sxs-lookup"><span data-stu-id="6f992-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="6f992-143">Załóżmy, że miała tooupdate tej tabeli:</span><span class="sxs-lookup"><span data-stu-id="6f992-143">Imagine you had tooupdate this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="6f992-144">oryginalne zapytanie Hello może sprawdzono podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="6f992-144">hello original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="6f992-145">Ponieważ Magazyn danych SQL nie obsługuje ANSI sprzężenia w hello `FROM` klauzuli `UPDATE` instrukcji, nie można skopiować ten kod nad zmieniając nieco.</span><span class="sxs-lookup"><span data-stu-id="6f992-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="6f992-146">Można użyć kombinacji `CTAS` i niejawne join tooreplace ten kod:</span><span class="sxs-lookup"><span data-stu-id="6f992-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="6f992-147">Zastępuje sprzężenia ANSI usunąć — instrukcje</span><span class="sxs-lookup"><span data-stu-id="6f992-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="6f992-148">Czasami najlepszym podejściem hello związanych z usuwaniem danych jest toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="6f992-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="6f992-149">Zamiast usuwania danych powitania po prostu wybierz hello dane, które mają tookeep.</span><span class="sxs-lookup"><span data-stu-id="6f992-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="6f992-150">To szczególnie istotne dla `DELETE` instrukcji używających ansi dołączenie składni, ponieważ usługa SQL Data Warehouse nie obsługuje sprzężeń ANSI w hello `FROM` klauzuli `DELETE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="6f992-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="6f992-151">Przykład przekonwertowanego instrukcji DELETE jest dostępny poniżej:</span><span class="sxs-lookup"><span data-stu-id="6f992-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="6f992-152">Zastąp instrukcjach merge</span><span class="sxs-lookup"><span data-stu-id="6f992-152">Replace merge statements</span></span>
<span data-ttu-id="6f992-153">Instrukcje scalania można zastąpić, co najmniej w części, za pomocą `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="6f992-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="6f992-154">Można skonsolidować hello `INSERT` i hello `UPDATE` w jednej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="6f992-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="6f992-155">Rekordy usunięte potrzebny toobe zamknięte w drugim instrukcji.</span><span class="sxs-lookup"><span data-stu-id="6f992-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="6f992-156">Przykład `UPSERT` znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="6f992-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="6f992-157">Zalecenie CTAS: jawnie określać typ danych i dopuszczanie wartości null dla danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="6f992-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="6f992-158">Podczas migrowania kod może się okazać, czy uruchomione przez ten typ kodowania wzorca:</span><span class="sxs-lookup"><span data-stu-id="6f992-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="6f992-159">Instynktownie może traktować ten kod tooa CTAS należy zmigrować, a użytkownik będzie poprawna.</span><span class="sxs-lookup"><span data-stu-id="6f992-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="6f992-160">Istnieje jednak jest ukrytym problem.</span><span class="sxs-lookup"><span data-stu-id="6f992-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="6f992-161">Witaj następujący kod nie uzyskanie takiego samego wyniku hello:</span><span class="sxs-lookup"><span data-stu-id="6f992-161">hello following code does NOT yield hello same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="6f992-162">Zwróć uwagę, hello kolumny "wynik" przenosi do przodu hello wartości typu i dopuszczanie wartości null danych hello wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="6f992-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="6f992-163">Może to prowadzić odchylenia toosubtle wartości, jeśli nie są dokładne.</span><span class="sxs-lookup"><span data-stu-id="6f992-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="6f992-164">Spróbuj następujących hello na przykład:</span><span class="sxs-lookup"><span data-stu-id="6f992-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="6f992-165">wartość Hello przechowywane dla wyniku różni się.</span><span class="sxs-lookup"><span data-stu-id="6f992-165">hello value stored for result is different.</span></span> <span data-ttu-id="6f992-166">Jak hello utrwalonego wartości w kolumnie wyników hello jest używany w innych wyrażenia hello błąd staje się jeszcze bardziej znaczące.</span><span class="sxs-lookup"><span data-stu-id="6f992-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="6f992-167">Jest to szczególnie ważne w przypadku migracji danych.</span><span class="sxs-lookup"><span data-stu-id="6f992-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="6f992-168">Mimo że hello drugiego zapytania jest raczej dokładniejsze występuje problem.</span><span class="sxs-lookup"><span data-stu-id="6f992-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="6f992-169">Hello dane byłyby różnych toohello porównaniu systemu źródłowego i powodująca tooquestions integralności w hello migracji.</span><span class="sxs-lookup"><span data-stu-id="6f992-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="6f992-170">Jest to jedna z rzadkich przypadkach gdy odpowiedzi "nieprawidłowe" hello jest rzeczywiście hello prawo jeden!</span><span class="sxs-lookup"><span data-stu-id="6f992-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="6f992-171">Witaj Przyczyna widzimy tej różnicy między wyniki hello dwa działa tooimplicit typu rzutowania.</span><span class="sxs-lookup"><span data-stu-id="6f992-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="6f992-172">Witaj pierwszej tabeli hello przykład definiuje hello definicji kolumny.</span><span class="sxs-lookup"><span data-stu-id="6f992-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="6f992-173">Po wstawieniu wiersza hello występuje niejawna konwersja typu.</span><span class="sxs-lookup"><span data-stu-id="6f992-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="6f992-174">W drugim przykładzie hello nie ma żadnych niejawna konwersja typu jako wyrażenie hello definiuje typ danych kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="6f992-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="6f992-175">Zwróć uwagę, również tej kolumny hello w drugim przykładzie hello została zdefiniowana jako kolumny wartości null należy w pierwszym przykładzie hello nie.</span><span class="sxs-lookup"><span data-stu-id="6f992-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="6f992-176">Podczas tworzenia tabeli hello w hello pierwszym przykładzie kolumny opcjami dopuszczania wartości null został jawnie zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="6f992-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="6f992-177">W drugim przykładzie hello został właśnie opuściła wyrażenie toohello i domyślnie spowodowałoby to w definicji wartości NULL.</span><span class="sxs-lookup"><span data-stu-id="6f992-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="6f992-178">tooresolve tych problemów, które należy jawnie ustawić konwersji typu hello i dopuszczanie wartości null hello `SELECT` część hello `CTAS` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="6f992-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="6f992-179">Nie można ustawić te właściwości w hello tworzenie części tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f992-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="6f992-180">Witaj w poniższym przykładzie pokazano, jak toofix hello kodu:</span><span class="sxs-lookup"><span data-stu-id="6f992-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="6f992-181">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6f992-181">Note hello following:</span></span>

* <span data-ttu-id="6f992-182">CAST lub CONVERT może zostały już użyte</span><span class="sxs-lookup"><span data-stu-id="6f992-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="6f992-183">ISNULL jest używane tooforce dopuszczania wartości null nie ŁĄCZONEJ</span><span class="sxs-lookup"><span data-stu-id="6f992-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="6f992-184">ISNULL jest najbardziej zewnętrzną funkcję hello</span><span class="sxs-lookup"><span data-stu-id="6f992-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="6f992-185">druga część hello ISNULL Hello jest stałą tj. 0</span><span class="sxs-lookup"><span data-stu-id="6f992-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="6f992-186">Dla poprawnie ustawić hello toobe dopuszczania wartości null jest istotne toouse `ISNULL` i nie `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="6f992-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="6f992-187">`COALESCE`nie jest deterministyczna funkcji i dlatego hello wynik hello wyrażenia zawsze będzie NULLable.</span><span class="sxs-lookup"><span data-stu-id="6f992-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="6f992-188">`ISNULL`różni się.</span><span class="sxs-lookup"><span data-stu-id="6f992-188">`ISNULL` is different.</span></span> <span data-ttu-id="6f992-189">Jest ona deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="6f992-189">It is deterministic.</span></span> <span data-ttu-id="6f992-190">W związku z tym jeśli hello drugiej części hello `ISNULL` funkcja jest stałą lub literałem, a następnie zostanie użyta wartość wynikową hello NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="6f992-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="6f992-191">Tej porady nie jest po prostu przydatne w przypadku zapewnienia integralności hello obliczeń.</span><span class="sxs-lookup"><span data-stu-id="6f992-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="6f992-192">Należy również do przełączenia partycji tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f992-192">It is also important for table partition switching.</span></span> <span data-ttu-id="6f992-193">Załóżmy, że w tej tabeli zdefiniowany jako Twoje fakt:</span><span class="sxs-lookup"><span data-stu-id="6f992-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="6f992-194">Pole wartości hello jest jednak wyrażenie obliczeniowej nie jest częścią hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6f992-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="6f992-195">toocreate partycjonowanej zestawu danych toodo może być to:</span><span class="sxs-lookup"><span data-stu-id="6f992-195">toocreate your partitioned dataset you might want toodo this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="6f992-196">Zapytanie Hello może działać dokładnie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="6f992-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="6f992-197">Hello problem jest dostarczany podczas próby tooperform hello partycji przełącznika.</span><span class="sxs-lookup"><span data-stu-id="6f992-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="6f992-198">definicje tabel Hello są niezgodne.</span><span class="sxs-lookup"><span data-stu-id="6f992-198">hello table definitions do not match.</span></span> <span data-ttu-id="6f992-199">definicje tabel hello toomake odpowiada hello CTAS musi toobe zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="6f992-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="6f992-200">Widać w związku z tym, że typ spójności i utrzymywanie właściwości dopuszczania wartości null na CTAS dobrej engineering najlepszym rozwiązaniem jest.</span><span class="sxs-lookup"><span data-stu-id="6f992-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="6f992-201">Pomaga integralności toomaintain w obliczeniach ono oraz gwarantuje również, że możliwe jest przełączanie partycji.</span><span class="sxs-lookup"><span data-stu-id="6f992-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="6f992-202">Przeczytaj tooMSDN, aby uzyskać więcej informacji na temat używania [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="6f992-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="6f992-203">Jest jednym z najważniejszych instrukcje hello w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6f992-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="6f992-204">Upewnij się, że rozumiesz dokładnie.</span><span class="sxs-lookup"><span data-stu-id="6f992-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f992-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f992-205">Next steps</span></span>
<span data-ttu-id="6f992-206">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="6f992-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
